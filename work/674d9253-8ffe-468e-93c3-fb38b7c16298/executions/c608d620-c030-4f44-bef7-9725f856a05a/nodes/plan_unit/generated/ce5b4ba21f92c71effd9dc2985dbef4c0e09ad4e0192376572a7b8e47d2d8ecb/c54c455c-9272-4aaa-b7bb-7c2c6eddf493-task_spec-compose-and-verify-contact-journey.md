---
task_id: compose-and-verify-contact-journey
depends_on: []
complexity: high
complexity_reason: The composed browser journey crosses independently built client, server, and persistent storage runtimes; pending, committed-success, storage-failure/retry, duplicate, boundary-validation, and restart behavior must remain consistent across the whole system.
implementation_constraints:
  - Own shared runtime composition in the root compose.yaml of https://github.com/demeedogg/backend-test-app.git (Backend Repository), based on the backend candidate rooted at main@e32f25d9ddb0612877f778f00e2de22bf0e1107c and the frontend candidate rooted at main@858555bf61e4c27218013d1d542bce07745fc16.
  - Compose the independently packaged frontend and backend images using their committed root build-manifest.json image references and include the persistent runtime dependency required by those candidates; do not prescribe a new API contract or add an external service.
  - Limit application-repository corrections to defects reproduced through the composed runtime; keep frontend corrections in the Frontend Repository and backend corrections in the Backend Repository.
  - Exercise submissions through browser form workflows only. Do not invoke a separately invented API operation or add an API operation identifier; no separate API specification is supplied.
  - Preserve exactly three pages, the Figma content and styling, anonymous access, duplicate acceptance, indefinite retention, and the absence of product-level frequency/record caps and excluded integrations.
  - Commit the composition and any runtime-reproduced corrections in their owning application repositories; when a correction changes image inputs, successfully rebuild that repository-local image and update its root build-manifest.json to the exact built image reference.
references:
  requirement_ids:
    - REQ-001
    - REQ-002
    - REQ-003
    - REQ-004
    - REQ-005
    - REQ-006
    - REQ-007
    - REQ-008
    - REQ-009
  design_references:
    - render-home-page-2-169
    - render-contact-form-page-2-200
    - render-confirmation-page-2-241
  openapi_operations: []
---

# Task: Compose and verify the complete contact journey

## Requirements satisfied

- REQ-001 — Verify the exactly-three-page journey and Home-to-form and return-to-Home transitions in the composed application; Confirmation is accessible only through a successful submission.
- REQ-002 — Verify the shared Details shell and all three page designs against the supplied renders, including the form's invalid state and the confirmation content.
- REQ-003 — Verify required Name and Email fields, validation boundaries and field-specific errors in the browser, with invalid input not persisted.
- REQ-004 — Verify that an accepted submission is stored before success is shown.
- REQ-005 — Verify repeated identical pairs create separate stored records and that persisted records have no expiry or scheduled deletion; confirm data survives a runtime restart.
- REQ-006 — Verify valid submissions are not rejected by a product-level frequency or record-count cap and that no cap-specific UI or rejection path is present.
- REQ-007 — Verify Confirmation is withheld while pending and after failure; backend failure leaves the visitor on the form with the exact required message and permits retry.
- REQ-008 — Verify Confirmation presents the actual submitted Name and Email and personalizes the greeting with the submitter's first name while retaining the Figma treatment.
- REQ-009 — Verify anonymous visitor access, exactly the three in-scope pages, and no excluded external integrations.

## Outcome

The Backend Repository contains a committed root `compose.yaml` that runs the delivered frontend and backend candidates with their required persistent runtime dependency. The complete application starts as one local composition and its user-observable contract and stored outcomes pass the assigned browser and persistence workflows. Any application defects corrected in this Task have first been reproduced in that composition and are committed to their owning application repositories. The composition is stopped and its resources are cleaned after verification.

## Behavioral contract

- Start the complete composition from the Backend Repository using the committed image references in the frontend and backend root `build-manifest.json` files, plus the storage/runtime dependency and persistent data configuration required by the candidates. The frontend must reach the backend through its configured internal connection. Do not use an external API, email service, analytics, authentication service, or other third-party integration.
- Use the browser to verify the Home, Contact Form, and Confirmation screens against `render-home-page-2-169`, `render-contact-form-page-2-200`, and `render-confirmation-page-2-241`, respectively. Preserve each render's copy, visual hierarchy, shared header/footer, active navigation treatment, colors, controls, and icons. The confirmation render's example data is replaced by the actual submitted values as required by REQ-008.
- Verify Home's “Go to contact form” action and Contact navigation open the form; the form's and Confirmation's “Back to home” actions return to Home. Only the successful form-submission flow can reveal Confirmation. No fourth product page is exposed.
- Use actual browser form submission for every submission workflow. Inspect the composed persistent store through its local repository-native/runtime mechanism to establish stored outcomes; do not make direct API requests as a substitute for a browser workflow.
- Invalid form submissions show errors below each affected field and do not create stored records. Use the Figma invalid-email copy exactly; required-field and Name errors identify their field and failed criterion.
- A successful backend storage result is the only success path. A pending or failed request does not show Confirmation. A backend failure keeps the visitor on the form and displays exactly “Unable to submit your information. Please try again.” without claiming that nothing was stored; a subsequent valid retry can succeed.
- Identical valid pairs are separate accepted submissions. There is no product-level request-frequency or total-record cap. Stored rows have no configured expiry or scheduled deletion and persist across a normal application/composition restart with its persistent data retained. The physical capacity of the chosen store is finite and is not claimed to be unlimited.

## Implementation approach

1. Inspect the delivered frontend and backend candidate outcomes, both candidate image manifests, and the selected backend storage/runtime configuration. In the Backend Repository, implement the root `compose.yaml` using the exact committed image references, required service dependencies, local network/configuration, and persistent data path. Keep each app's independent image buildability intact; do not substitute source-mounted development servers for the packaged candidate images.
2. Start the complete composition and wait until the frontend, backend, and persistent runtime dependency are ready. Record the startup and shutdown procedure in the Backend Repository's composition documentation or README, including the persistent data path and cleanup behavior.
3. Exercise all page transitions and compare each rendered screen/state with its cited design render at the same reference viewport. Verify page copy, controls, shared frame, active navigation, invalid-email styling and message, confirmation styling, submitted values, and all return actions.
4. Through the browser, submit an empty form and malformed values, then valid boundary values: Name lengths 1 and 100, and a syntactically valid Email of 254 characters. Verify Name length 0/101 and Email length 255 are rejected at their respective fields, required-field errors appear below the fields, and invalid submissions create no stored rows. For the malformed email state, verify the exact copy “Enter a valid email address, like alex@example.com.”
5. Through the browser, submit a valid pair and confirm the browser reaches Confirmation only after the corresponding pair is visible in persistent storage. Confirm the screen displays the exact submitted name and email and uses the submitted first name in the thank-you sentence. Submit the identical pair again and verify another distinct stored row is created and the flow succeeds again.
6. Exercise backend failure by making the composed backend/storage dependency unavailable using the composition's local controls, then submit valid data in the browser. Verify the visitor remains on the form with the exact failure message and can retry after service recovery. Do not infer from the failure response that a record was not stored; inspect resulting rows and account for the allowed ambiguous post-commit failure. Verify no runtime configuration, validation path, or repeated-submission behavior implements a request-frequency or total-record cap; practical repeated submits are behavioral samples, not proof of infinite capacity.
7. Restart the composition while retaining its configured persistent data and verify prior accepted rows remain. Inspect the server/store configuration for expiry, TTL, scheduled deletion, or application-level rate/record limits and confirm none is present. Verify no login/authorization prompt, additional page, volume-limit UI, or excluded external integration is introduced.
8. Correct only defects reproduced through the composed runtime. Place a frontend fix in the Frontend Repository and a backend or persistence fix in the Backend Repository. Run the owning repository's focused verification; if a correction changes application or runtime image inputs, build the affected standalone image successfully and update its `build-manifest.json` with the exact built image reference. Commit composition, relevant image manifests, and reproduced fixes in their owning candidate repositories.
9. After all checks pass, stop the composition and clean its transient containers/network while following the documented persistent-data policy. Confirm the final repository state includes the committed composition and all required candidate commits/manifests.

## Acceptance criteria

- The root `compose.yaml` in the Backend Repository starts the frontend and backend from their independently packaged image references and supplies the persistent runtime dependency/data path they require. The complete application becomes browser-accessible and can be stopped and cleaned using documented commands.
- Browser comparison confirms the Home, Contact Form, and Confirmation match the content, styling, and hierarchy of all three cited Figma renders, including shared Details branding/header/footer and the invalid-email presentation. The Home call to action and Contact navigation lead to the form; both “Back to home” actions lead to Home; no additional page is exposed.
- Submitting missing values, Name length 0 or 101, malformed Email, or Email length 255 produces field-specific errors below invalid fields and creates no valid stored submission. The malformed-email error uses exactly “Enter a valid email address, like alex@example.com.” Name lengths 1 and 100 and valid Email length 254 are accepted.
- A valid browser submission is stored as the submitted pair before Confirmation appears. Confirmation is not shown while the backend is pending or after an unsuccessful response. It displays the exact submitted Name and Email, personalizes the greeting with the submitter's first name, and returns to Home through “Back to home.”
- A backend failure leaves the browser on Contact Form and displays exactly “Unable to submit your information. Please try again.” A later retry can succeed. The verification does not treat a response lost after a committed write as evidence of no record.
- Repeating the same valid pair is accepted and creates a distinct stored record. The composed runtime and application configuration have no product-level request-frequency or total-record cap, no corresponding visitor rejection/message/page, and no expiry or scheduled deletion. Previously stored records remain after restarting the application with persistent data retained.
- The visitor flow requires no authentication or authorization and introduces no external APIs, email services, analytics, third-party integrations, or additional pages.
- All browser submissions in the verification use the UI form; storage is checked using local persistence/runtime inspection. No operation ID is invented or required because the indexed evidence contains no separate API specification.
- Runtime-reproduced application corrections and the root composition are committed in their owning application repositories. If any correction changes an image input, its standalone image build succeeds and the owning repository's committed root `build-manifest.json` matches that image. The completed composition is stopped and cleaned.

## Verification

- Start the documented composition and confirm service readiness, frontend-to-backend connectivity, and writable persistent storage. Confirm its frontend/backend image references agree with both candidate root `build-manifest.json` files.
- Run browser workflows for Home-to-Contact, Contact-to-Home, invalid form submission, valid boundary submissions, invalid boundaries, successful storage and Confirmation, identical-pair resubmission, backend failure and retry, and Confirmation-to-Home. Inspect the persistent store to verify row counts, values, invalid-input non-persistence, distinct duplicates, and survival after restart.
- Compare the three pages and required states to the source renders at a consistent viewport; confirm exact copy and field-error placement, no early Confirmation, actual confirmation values, and no extra page.
- Inspect the composed runtime configuration and relevant application configuration for authentication, external integrations, request-frequency/record caps, expiry, or scheduled deletion. Verify persistent data across restart without representing a finite sample as proof of unlimited physical capacity.
- Run focused repository-native verification for any runtime-reproduced application corrections, rebuild only affected standalone images when their inputs change, and inspect the corresponding committed manifests.
- Stop the composition and clean transient resources; verify the root composition and all affected application changes are committed in their assigned repositories.
