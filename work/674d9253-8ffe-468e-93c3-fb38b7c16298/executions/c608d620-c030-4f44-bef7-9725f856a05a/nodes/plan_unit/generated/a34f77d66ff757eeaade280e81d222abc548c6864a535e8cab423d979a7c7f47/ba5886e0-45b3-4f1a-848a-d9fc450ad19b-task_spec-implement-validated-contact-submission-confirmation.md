---
task_id: implement-validated-contact-submission-confirmation
depends_on: []
complexity: medium
complexity_reason: Field-boundary validation, asynchronous API outcomes, retryable failure state, and success-only navigation must stay consistent across the client/backend contract without exposing stale or incorrect submitted values.
implementation_constraints:
  - Work only in https://github.com/demeedogg/frontend-test-app.git, branch main, planned from commit 858555bf61e4c27218013d1d542bce07745fc16d.
  - Enforce the PRD's required Name (1–100 characters) and Email Address (valid format, at most 254 characters) rules on the client and keep client checks aligned with the backend prerequisite's whitespace, character-count, and syntax rules.
  - Use the internal submission contract delivered by backend-contact-submission-and-persistence; do not implement or modify server behavior or persistence.
  - Use the Figma invalid-email copy and field treatment, show the exact required backend-failure message, and expose Confirmation only after a successful backend response.
  - Preserve the exactly-three-page, anonymous, self-contained scope; add no external integrations or additional pages.
  - Preserve the standalone frontend image established by frontend-page-shell-and-navigation; for application or image-input changes, build that image successfully and replace the root build-manifest.json with its exact image name and tag.
references:
  requirement_ids:
    - REQ-001
    - REQ-002
    - REQ-003
    - REQ-007
    - REQ-008
    - REQ-009
  design_references:
    - render-contact-form-page-2-200
    - render-confirmation-page-2-241
  openapi_operations: []
---

# Task: Validate and complete the contact submission flow

## Requirements satisfied

- REQ-001 — Complete the Contact Form-to-Confirmation transition only for a successful submission and preserve the Confirmation return-to-Home action supplied by the page shell.
- REQ-002 — Match the form, invalid-email state, success confirmation, submitted-value summary, and return action to the cited Figma renders.
- REQ-003 — Validate required Name and Email Address values and their length/format constraints, presenting field-specific errors below invalid fields and preventing invalid submission.
- REQ-007 — Keep pending or failed requests on Contact Form; show the exact failure message after unsuccessful responses and allow retry.
- REQ-008 — On success, show the submitted Name and Email and personalize the confirmation sentence with the submitter's first name.
- REQ-009 — Keep this client flow unauthenticated and within the three specified pages, without external integrations.

## Outcome

Visitors can enter and submit valid contact details through the existing frontend shell. Invalid values receive actionable feedback without a request. Confirmation is rendered only after the backend reports success, and it summarizes the exact submitted pair; unsuccessful requests leave the entered values available for retry and display the required failure message.

## Behavioral contract

- Contact Form contains labeled Name and Email Address fields, the required-fields note, the “Submit details” action, the existing return-to-Home action, privacy reassurance, and the shared shell. Start with empty fields; the sample values in the render are illustrative, not visitor defaults.
- Validate on submission. Name and Email are both required; a whitespace-only value is treated as missing, length is counted consistently with the backend contract, Name accepts 1–100 characters, and Email must pass the backend-aligned syntax check and be no longer than 254 characters. Preserve the entered strings when submitting and displaying the successful summary.
- Show each field error below its field. Use concise field- and criterion-specific copy for required and Name-length errors, and use the exact Figma invalid-email copy: “Enter a valid email address, like alex@example.com.” Apply the rendered red invalid-field treatment to the invalid Email state. Clear an error when the corrected value is valid or when the form is revalidated.
- Do not send a request while client validation fails. Submit valid values using the backend prerequisite's internal contract: `POST /api/contact-submissions` with JSON fields `name` and `email`; treat only HTTP `201 Created` with the documented JSON body `{"id": <integer>}` as success. Treat other statuses, malformed/unexpected bodies, and network errors as failure. Do not add a uniqueness check or client-side frequency/record cap.
- While a request is pending, remain on Contact Form and do not expose Confirmation. A transient pending affordance may prevent repeated activation of that same in-flight submission; after it settles, allow a new valid submission, including an identical pair.
- On failure, remain on Contact Form, preserve the entered values, and display exactly “Unable to submit your information. Please try again.” The message does not claim that the backend stored nothing. A subsequent valid retry follows the same pending/success/failure behavior.
- On success, pass the submitted pair into the existing guarded Confirmation view. Render the actual Name and Email rather than the samples, keep the confirmation copy and Figma card/check-icon/summary styling, and replace “Alex” in the thank-you sentence with the submitter's first name. For names with leading whitespace or multiple words, use the first non-whitespace token as the first name and preserve the full original name in the summary. “Back to home” returns to Home.
- Use the existing frontend configuration convention for the backend origin; if none exists, establish and document one minimal configurable internal-service origin. The client tests and image build must not require a running backend. Do not add routes or third-party integrations.

## Implementation approach

1. Inspect the frontend shell and existing form/Confirmation integration seam delivered by `frontend-page-shell-and-navigation`, and use its local scripts, dependencies, state guard, and image conventions. The pinned frontend repository was an empty starter, so follow the selected stack and versions established by that prerequisite rather than introducing another runtime.
2. Implement a focused client validator for required values, Name length, Email syntax and length. Align blank handling and character counting with the backend Task's contract; keep error copy field-specific, place it below each field, and retain raw input values.
3. Add the frontend API-client call to the backend Task's `POST /api/contact-submissions` contract. Handle only the documented success status as success; map all unsuccessful/network outcomes to the form-level error and keep the form retryable. Keep the origin configurable according to the existing frontend convention and document the selected default if one must be added.
4. Connect validated success to the existing success-guarded Confirmation view, passing the actual submitted pair and deriving the personalized first name without changing the shared shell or adding pages.
5. Add hermetic client tests with controlled API responses. Cover validation, blocked invalid submissions, pending state, success-only route transition, unsuccessful and network outcomes, exact failure copy, retained values and retry, duplicate retry allowance, actual-pair rendering, first-name personalization, and the Confirmation return action. Add a focused visual comparison/render check for the form's invalid-email treatment and Confirmation against the cited renders.
6. Run the repository-native client tests and production build. Since this Task changes application/image inputs, successfully build the standalone frontend image without starting a container or requiring the backend, then replace the repository-root `build-manifest.json` with the exact built image name and tag. Verify the client image remains independently buildable.

## Acceptance criteria

- Empty/whitespace-only Name or Email, Name length 0 or over 100, malformed Email, and Email over 254 characters produce field-specific errors below affected fields and cause no API request. Valid Name lengths 1 and 100, and a syntactically valid Email of length 254, pass client validation.
- The rendered malformed-email state uses “Enter a valid email address, like alex@example.com.” and the Figma red field/icon treatment. Missing-field and Name-length messages identify their field and criterion.
- Submitting valid values sends exactly the entered Name and Email through the backend prerequisite's internal contract. Pending or unsuccessful outcomes never show Confirmation; only the documented successful response does.
- A backend error response or network failure leaves the visitor on Contact Form, preserves the entered values, and shows exactly “Unable to submit your information. Please try again.” A later valid retry can succeed; repeated identical values are not blocked client-side.
- After success, Confirmation displays the exact submitted pair and the personalized first-name greeting in the Figma treatment, and “Back to home” returns to Home. Confirmation cannot be reached through a failed or still-pending submission.
- The client continues to expose only Home, Contact Form, and Confirmation, with no authentication or external integration added.
- Focused repository-native tests and production build pass. The standalone frontend image builds without starting a container or requiring a backend; after that successful build, root `build-manifest.json` contains the exact image name and tag built by this Task.

## Verification

- Run the documented frontend-native test command and inspect coverage for required/whitespace, lengths 1/100/101, valid Email length 254, malformed/overlong Email, field-specific error placement, and zero requests for invalid input.
- Use controlled HTTP responses to verify pending, HTTP 201 success, non-success response, unexpected response, network failure, exact failure copy, retained input, retry, no duplicate suppression, successful routing, actual-pair display, personalized greeting, and return-to-Home behavior. These tests must not start the backend or rely on external network services.
- Run the repository's production build and focused visual check for `render-contact-form-page-2-200` and `render-confirmation-page-2-241`.
- Build the standalone frontend runtime image without starting it; inspect the resulting configuration and confirm it does not require the backend to build or serve the client shell.
- Inspect the frontend root `build-manifest.json` and confirm its image name and tag exactly match the successfully built image.
