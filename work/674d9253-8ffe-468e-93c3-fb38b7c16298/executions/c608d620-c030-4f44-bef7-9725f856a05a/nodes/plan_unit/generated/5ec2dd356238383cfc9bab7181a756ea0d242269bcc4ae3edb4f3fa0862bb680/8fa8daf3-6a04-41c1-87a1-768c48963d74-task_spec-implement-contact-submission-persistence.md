---
task_id: implement-contact-submission-persistence
depends_on: []
complexity: high
complexity_reason: The success status must follow a committed SQLite write while preserving separate duplicate rows, and validation, database failures, restart persistence, and a standalone non-root image all need hermetic verification from a previously empty backend snapshot.
implementation_constraints:
  - Work only in https://github.com/demeedogg/backend-test-app.git, branch main, planned from commit e32f25d9ddb0612877f778f00e2de22bf0e1107c.
  - Enforce the PRD's required Name (1–100 characters) and valid Email Address (at most 254 characters) constraints on the server; invalid input must not be stored as a valid submission.
  - Accept every valid submission, including identical repeats; retain accepted pairs without expiry or scheduled deletion and do not add a product-level request-frequency or total-record cap.
  - Keep the visitor flow anonymous and the backend self-contained: add no authentication, external APIs, email services, analytics, or third-party service integrations.
  - Keep changes within backend behavior, its internal submission contract, persistence, repository-local runtime packaging, documentation, and backend-local verification; do not change frontend code or application composition.
  - As this backend repository's first feature-bearing Task, provide its standalone version-pinned non-root runtime image, startup configuration, build-context exclusions, local image-build documentation, and root build-manifest.json update required by the Delivery unit.
references:
  requirement_ids:
    - REQ-003
    - REQ-004
    - REQ-005
    - REQ-006
    - REQ-007
    - REQ-009
  design_references: []
  openapi_operations: []
---

# Task: Accept and durably persist valid contact submissions

## Requirements satisfied

- REQ-003 — Independently validate required Name and Email values on the server, enforce Name length 1–100 and Email syntax/maximum length 254, and reject invalid submissions without storing them.
- REQ-004 — Store every accepted Name/Email pair and return success only after persistence has committed; report genuine validation, processing, or storage failures as unsuccessful outcomes.
- REQ-005 — Store identical valid pairs as separate submissions and retain records without expiry or scheduled deletion.
- REQ-006 — Do not reject valid submissions based on request frequency or total record count.
- REQ-007 — Expose an unambiguous successful response only after processing and storage succeed; return an unsuccessful response when validation or storage fails so the client can remain on its form and display the product's specified failure message.
- REQ-009 — Keep this internal backend capability unauthenticated and free of excluded external integrations.

## Outcome

The empty backend destination provides a documented internal submission contract and a standalone HTTP service that accepts, validates, and durably stores anonymous Name/Email pairs. The service preserves each accepted pair as an independent record, including exact repeats, and its positive response means the database transaction committed. The repository can be tested and its non-root runtime image built without the frontend or a running database/service.

## Behavioral contract

- Implement `POST /api/contact-submissions` accepting `application/json` with string fields `name` and `email`.
- For a valid request, commit one new record and return HTTP `201 Created` with JSON `{"id": 1}`, where `id` is the generated integer record identifier. Do not return success before the commit completes.
- Reject missing or non-string fields, empty or whitespace-only Name/Email values, Name values outside 1–100 characters, malformed Email values, and Email values longer than 254 characters with HTTP `400 Bad Request` and JSON of the form `{"error":"invalid_submission","fieldErrors":{"name":"required","email":"invalid_format"}}`, including only applicable field-error entries. Each invalid field maps to one string code: `name` uses `required`, `invalid_type`, or `invalid_length`; `email` uses `required`, `invalid_type`, `invalid_format`, or `invalid_length`. Malformed JSON or a non-object body returns the same error code with an empty `fieldErrors` object; a non-JSON content type returns HTTP `415` with `{"error":"unsupported_media_type"}`. Invalid input never creates a record.
- Report an actual processing or persistence failure with HTTP `500` and `{"error":"submission_failed"}`, without exposing database details. Do not convert a failed write into a successful response. A response lost after a successful commit is inherently ambiguous to the caller; a retry may create another record, which is allowed.
- Preserve the input strings in storage rather than canonicalizing case or trimming the submitted values. As a conventional detail for unspecified blank handling and character counting, reject a Name or Email that is empty or whitespace-only after trimming for the required check, enforce Name and Email lengths by Unicode code points, and persist the original values. Validate the untrimmed Email string's address syntax without DNS, mailbox ownership, or deliverability checks.
- Use SQLite as the internal persistence default, with a configurable database-file path. Create a table with a generated primary key and non-unique Name and Email columns. Commit each accepted submission before responding; use no uniqueness constraint, deduplication, expiry, scheduled deletion, request-rate limiter, or total-record cap. Configure a persistent writable data path for the runtime image and document how local operators mount/preserve it across container replacement; do not claim physical capacity is infinite.
- Use Python 3.12, Flask, SQLite, and a syntax-only email validation library as the conventional greenfield runtime defaults. Pin dependency versions in a committed lock/requirements file and pin the image base to an exact Python 3.12 patch release and digest (never a floating `latest` tag). Run the service with a production WSGI server as a non-root user. No external service is required at runtime.

## Implementation approach

1. Establish the smallest backend project structure consistent with the empty `README.md`-only snapshot. Document the chosen runtime and the internal HTTP request, success, validation-error, and processing/storage-error shapes above so the dependent frontend unit can consume the contract without inventing endpoints or response behavior.
2. Implement the Flask submission handler and server-side validator. Check request shape and field constraints before invoking persistence. Keep any syntax validation local; do not perform email deliverability lookup, account checks, authentication, external calls, or rate/record counting.
3. Add a small SQLite persistence layer whose schema has no uniqueness constraint on the submitted pair and no expiration/deletion mechanism. Make the database path configurable for tests and runtime use. Treat transaction commit as the success boundary and convert genuine persistence exceptions into an unsuccessful server response.
4. Add repository-native hermetic tests using Flask's test client and temporary SQLite files. Exercise missing and malformed input, all length boundaries, invalid-value non-persistence, successful commit, duplicate insertion, database reopening/restart persistence, and injected storage failure. Keep tests independent of network services and the frontend.
5. Add a standalone multi-stage or otherwise minimal runtime image using the exact pinned Python base, non-root runtime user, explicit startup configuration, and `.dockerignore` exclusions. Configure the writable SQLite data path without requiring a database container. Document local setup, test, image-build, and persistent-volume commands in the backend README.
6. Run the documented backend tests and build the repository-local image without starting a container or requiring the frontend/database service. After a successful build, replace the backend repository root `build-manifest.json` with a minimal JSON object containing the exact built image reference as `{"image":"<image-name>:<tag>"}`, and document this format in the README.

## Acceptance criteria

- The documented `POST /api/contact-submissions` accepts a valid JSON pair without authentication and returns `201` only after a database commit; its success body is `{"id": <integer>}`. Validation responses use the specified stable `error` and `fieldErrors` shape and one of the documented field codes, malformed JSON/non-object payloads return an empty `fieldErrors` object, unsupported content types return `415`, and processing/storage failures return HTTP `500` with `{"error":"submission_failed"}`.
- Server-side validation rejects absent/non-string values, empty or whitespace-only Name/Email, Name length 0 or greater than 100, malformed Email, and Email length greater than 254. Rejected requests return a non-success validation response and leave the database unchanged.
- Valid Name values of 1 and 100 characters and a syntactically valid Email of exactly 254 characters are accepted and stored; test fixtures demonstrate these exact boundaries. Email values exceeding 254 characters are rejected.
- A successful submission can be read back from the SQLite file after closing and reopening the application/database. No expiry or scheduled deletion is configured.
- Submitting the same valid Name/Email pair twice returns success twice and creates two distinct rows. Neither a uniqueness constraint nor deduplication logic suppresses the second row.
- An injected database write/commit failure returns an unsuccessful server response, never a success response, and does not leave a committed row for a failed transaction. The response does not reveal internal database details; the API does not promise that a client-observed failure means no row exists if the commit succeeded and only the response was lost.
- The service contains no authentication/authorization, external API, email delivery, analytics, third-party integration, application-level request-frequency cap, or total-record cap.
- Focused backend-native tests pass using temporary local storage and no external service. The standalone image builds successfully from this repository without starting a container, frontend, or database service; the runtime is pinned and configured to run as non-root with a writable configurable database path.
- The backend README documents the contract, selected runtime/persistence assumptions, local test and image-build commands, data-volume configuration, and build-manifest format. The root `build-manifest.json` contains `{"image":"<image-name>:<tag>"}` for the exact image successfully built by this Task.

## Verification

- Run the documented backend-native test command. Confirm tests cover Name lengths 1, 100, 0, and 101; valid Email length 254; invalid and overlong Email; missing/non-string fields; no persistence on validation failure; successful persistence; duplicate acceptance; reopening the database; and injected persistence/commit failure.
- Inspect the created temporary SQLite rows in the tests to verify that a successful result follows commit, each duplicate creates a separate row, invalid input creates none, and restart/reopen retains prior rows.
- Build the documented repository-local runtime image without starting it or requiring the frontend or any database/service. Inspect the image configuration for an exact pinned Python base, non-root execution, configured startup, and writable database directory.
- Inspect `.dockerignore`, the README's contract and local commands, and the root `build-manifest.json`; confirm the manifest's image name/tag exactly matches the successful build.
