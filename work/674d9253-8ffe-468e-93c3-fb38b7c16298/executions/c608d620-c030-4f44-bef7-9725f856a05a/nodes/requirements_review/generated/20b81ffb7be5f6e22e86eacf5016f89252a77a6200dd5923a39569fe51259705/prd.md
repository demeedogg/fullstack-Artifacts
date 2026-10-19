# Product requirements document: Artifact's Repo test

## Requested outcome

Deliver a minimal, visitor-facing contact-form application that follows the supplied Details Figma design, collects a visitor's name and email address, stores each correctly submitted pair through the application backend, and confirms the submission only after successful backend processing.

## Scope

- Exactly three pages: Home, Contact Form, and Confirmation.
- A Figma-aligned presentation and navigation for those pages, including the specified form, validation feedback, success summary, and return actions.
- Anonymous name/email submissions, storage of each valid pair, duplicate acceptance, and the specified success and failure outcomes.
- Indefinite retention and no product-level request-frequency or total-record limit, as resolved by the human clarifications.
- The Work assigns `https://github.com/demeedogg/frontend-test-app.git` (`DESTINATION`, frontend application code, branch `main`) and `https://github.com/demeedogg/backend-test-app.git` (`DESTINATION`, backend application code, branch `main`). These identify the intended application destinations, not product technology requirements.

## Out of scope

- Authentication, authorization, accounts, or an administrative interface.
- Additional pages, including a retention-disclosure or volume-limit page.
- External APIs, email services, analytics, or other third-party integrations.
- Email ownership or deliverability verification, notifications, or recipients beyond the application backend.
- Manual deletion, scheduled expiry, deduplication, or a product-level request/record cap.
- An API specification or implementation-specific storage, deployment, or architecture decisions.

## Requirements

### REQ-001 — Three-page contact journey

**Requirement:** The application must provide exactly Home, Contact Form, and Confirmation pages. Home's “Go to contact form” action opens Contact Form; the form's and Confirmation's “Back to home” actions return to Home. Confirmation is reached through the successful-submission flow only.

**Acceptance:**
- A visitor can use the Home call to action to reach Contact Form.
- “Back to home” on Contact Form and Confirmation returns the visitor to Home.
- The application exposes no additional page, and Confirmation is shown only after the successful backend outcome in REQ-007.

**Evidence:** Work `674d9253-8ffe-468e-93c3-fb38b7c16298` (exactly-three-pages and navigation clauses); `design-description` (`render-home-page-2-169`, `render-contact-form-page-2-200`, `render-confirmation-page-2-241`); `review:requirements` Artifact `2a04185d-3c75-40e4-9a84-6b145fb9e205`; `review:frontend` Artifact `b1c0b5b6-8811-4b21-9ff7-bce1b5637777`.

**Decision provenance:** Approved AFU Artifact `2a04185d-3c75-40e4-9a84-6b145fb9e205`; contributing subjects `AFU-REQ-001`, `AFU-AC-001`.

**Supersedes:** None

### REQ-002 — Follow the supplied Figma design

**Requirement:** The three pages must preserve the Figma design's content, styling, and visual hierarchy. This includes Details branding; the white header with Home and Contact navigation and active-section treatment; pale neutral backgrounds; centered white content panels/cards; dark headings, muted supporting text, green accents and icons; the page-specific copy and controls; and the shared footer copy “© 2026 Details” and “A little information. A simple connection.” The privacy reassurance “Your details stay private and secure.” is design copy and does not establish a separate security control.

**Acceptance:**
- Home presents the design's introduction, supporting copy, “Go to contact form” action, and privacy reassurance.
- Contact Form presents the “Your contact details” content, required-fields note, labeled Name and Email fields, “Submit details” action, return action, and privacy reassurance.
- Confirmation presents the success icon, “You’re all set!” heading, confirmation message, submitted-pair summary, “Back to home” action, and shared header/footer in the Figma treatment.

**Evidence:** Work `674d9253-8ffe-468e-93c3-fb38b7c16298` (Figma-fidelity clause); `design-description` lines 9–62; `review:requirements` Artifact `2a04185d-3c75-40e4-9a84-6b145fb9e205`; `review:frontend` Artifact `b1c0b5b6-8811-4b21-9ff7-bce1b5637777`.

**Decision provenance:** Approved AFU Artifact `2a04185d-3c75-40e4-9a84-6b145fb9e205`; contributing subject `AFU-REQ-002`.

**Supersedes:** None

### REQ-003 — Validate required contact details

**Requirement:** Name and Email Address must both be provided. Name must contain 1–100 characters. Email must use a valid email format and contain no more than 254 characters. Each invalid field must display its own validation error below that field, and invalid or incomplete values must not be treated or stored as a valid submission. Use the Figma's exact invalid-email copy, “Enter a valid email address, like alex@example.com.” For required-field and Name errors, use concise field- and criterion-specific copy. Validation occurs on submission; an error may be cleared when the value is corrected or revalidated.

**Acceptance:**
- Missing Name or Email, a Name outside 1–100 characters, malformed Email, or Email longer than 254 characters is identified beneath the affected field and cannot proceed as a valid submission.
- Name lengths of 1 and 100 characters and valid Email length of 254 characters are accepted at the boundaries.
- The invalid-email example uses the Figma copy and treatment; errors identify the affected field.

**Evidence:** Work `674d9253-8ffe-468e-93c3-fb38b7c16298` (field constraints and feedback); `design-description` lines 37–39 and 64–66; `review:requirements` Artifact `2a04185d-3c75-40e4-9a84-6b145fb9e205`; `review:frontend` Artifact `b1c0b5b6-8811-4b21-9ff7-bce1b5637777`; `review:backend` Artifact `f41451e3-d1e1-4da9-a2d5-fd6962862e31`.

**Decision provenance:** Approved AFU Artifact `2a04185d-3c75-40e4-9a84-6b145fb9e205`; contributing subjects `AFU-RULE-003`, `AFU-REQ-007`, `AFU-AC-002`.

**Supersedes:** None

### REQ-004 — Store each correctly submitted pair

**Requirement:** For each correctly submitted Name and Email pair that the backend accepts, the backend must store the submitted pair. A successful outcome must mean the pair has been stored. Invalid or incomplete pairs must not be stored as valid submissions.

**Acceptance:**
- A correctly submitted pair that receives a successful outcome is stored as a name/email pair.
- A submission that fails the required-field, length, or email-format rules is not accepted as a valid submission or stored as one.
- The success outcome used by the visitor flow corresponds to successful storage, not merely receipt of form input.

**Evidence:** Work `674d9253-8ffe-468e-93c3-fb38b7c16298` (backend storage and validation clauses); `review:requirements` Artifact `2a04185d-3c75-40e4-9a84-6b145fb9e205`; `review:backend` Artifact `f41451e3-d1e1-4da9-a2d5-fd6962862e31`; supporting repository evidence `analysis:backend-test-app-7cad18d3`.

**Decision provenance:** Approved AFU Artifact `2a04185d-3c75-40e4-9a84-6b145fb9e205`; contributing subjects `AFU-REQ-006`, `AFU-RULE-003`, `AFU-AC-003`, `AFU-AC-006`.

**Supersedes:** None

### REQ-005 — Accept duplicates and retain submissions indefinitely

**Requirement:** Identical name/email pairs must be accepted as separate submissions; equality with an earlier pair must not reject or suppress a submission. Retain every stored pair indefinitely, without time-based expiry or scheduled deletion. This does not add a manual deletion feature or promise immunity from physical storage failure.

**Acceptance:**
- Repeating an identical valid submission is accepted and results in a separate stored submission.
- Stored pairs do not expire or undergo scheduled deletion.

**Evidence:** Work `674d9253-8ffe-468e-93c3-fb38b7c16298` (duplicate allowance); Clarification `3b8b55fe-35cd-40ab-b6e9-dd880294df56` (indefinite retention); `review:requirements` Artifact `2a04185d-3c75-40e4-9a84-6b145fb9e205`; `review:frontend` Artifact `b1c0b5b6-8811-4b21-9ff7-bce1b5637777`; `review:backend` Artifact `f41451e3-d1e1-4da9-a2d5-fd6962862e31`.

**Decision provenance:** Approved AFU Artifact `2a04185d-3c75-40e4-9a84-6b145fb9e205`; contributing subjects `AFU-RULE-004`, `AFU-RULE-005`, `AFU-AC-003`.

**Supersedes:** None

### REQ-006 — Do not impose product-level volume limits

**Requirement:** The application must not impose a request-frequency limit or total-record limit that rejects an otherwise valid submission. A genuine backend or storage failure remains a failure under REQ-007; this requirement does not assert infinite physical capacity.

**Acceptance:**
- Submission frequency or current record count alone does not reject a valid submission.
- No volume-limit-specific page, message, or rejection path is presented.
- A genuine backend failure is handled by REQ-007 rather than represented as an application-level cap.

**Evidence:** Clarification `150307b3-b364-4f42-94cb-c912a02f9119` (no request-frequency or total-record limit); Work `674d9253-8ffe-468e-93c3-fb38b7c16298`; `review:requirements` Artifact `2a04185d-3c75-40e4-9a84-6b145fb9e205`; `review:frontend` Artifact `b1c0b5b6-8811-4b21-9ff7-bce1b5637777`; `review:backend` Artifact `f41451e3-d1e1-4da9-a2d5-fd6962862e31`.

**Decision provenance:** Approved AFU Artifact `2a04185d-3c75-40e4-9a84-6b145fb9e205`; contributing subject `AFU-RULE-006`, `AFU-AC-004`.

**Supersedes:** None

### REQ-007 — Report submission success and failure accurately

**Requirement:** Show Confirmation only after the visitor receives a successful backend outcome indicating successful processing and storage. On backend failure, remain on Contact Form and display exactly: “Unable to submit your information. Please try again.” The visitor can correct or retry from the form. A failure message does not promise that no pair was stored if storage succeeded but its success response was not observed; a retry may therefore create a duplicate under REQ-005.

**Acceptance:**
- A pending or unsuccessful backend outcome does not display Confirmation.
- A successful backend outcome leads to Confirmation.
- A backend failure leaves the visitor on Contact Form with exactly the specified message and permits a subsequent valid retry.
- The failure message does not assert that the backend stored nothing.

**Evidence:** Work `674d9253-8ffe-468e-93c3-fb38b7c16298` (submission outcome and exact failure behavior); `design-description` lines 33–42; `review:requirements` Artifact `2a04185d-3c75-40e4-9a84-6b145fb9e205`; `review:frontend` Artifact `b1c0b5b6-8811-4b21-9ff7-bce1b5637777`; `review:backend` Artifact `f41451e3-d1e1-4da9-a2d5-fd6962862e31`.

**Decision provenance:** Approved AFU Artifact `2a04185d-3c75-40e4-9a84-6b145fb9e205`; contributing subjects `AFU-REQ-008`, `AFU-REQ-009`, `AFU-AC-005`. The possible stored-pair outcome after an unobserved success and the resulting duplicate on retry are a deduction recorded in the AFU registry for `AFU-REQ-009`.

**Supersedes:** None

### REQ-008 — Show the submitted values on Confirmation

**Requirement:** Confirmation must use the Figma's confirmation content and styling while showing the actual submitted Name and Email, not the render's sample values. Replace the sample first name in the thank-you sentence with the submitter's first name while preserving the sentence's meaning and styling.

**Acceptance:**
- After a successful submission, Confirmation summarizes the exact submitted name and email.
- The thank-you sentence refers to the submitter by their first name rather than displaying the sample name “Alex” for another visitor.
- The confirmation layout and visual treatment remain aligned with Figma.

**Evidence:** Work `674d9253-8ffe-468e-93c3-fb38b7c16298` (success-only confirmation and Figma fidelity); `design-description` lines 9–22 and 64–66; `review:requirements` Artifact `2a04185d-3c75-40e4-9a84-6b145fb9e205`; `review:frontend` Artifact `b1c0b5b6-8811-4b21-9ff7-bce1b5637777`; `review:backend` Artifact `f41451e3-d1e1-4da9-a2d5-fd6962862e31`.

**Decision provenance:** Approved AFU Artifact `2a04185d-3c75-40e4-9a84-6b145fb9e205`; contributing subjects `AFU-REQ-010`, `AFU-AC-005`. The actual-pair summary and personalized first name are recorded in the AFU provenance registry as deduction and minor-detail decisions, respectively.

**Supersedes:** None

### REQ-009 — Keep the experience unauthenticated and self-contained

**Requirement:** Visitors must be able to view the pages, enter and submit the two fields, and use the specified navigation without authentication or authorization. Do not add external APIs, email services, analytics, third-party services or integrations, or additional pages.

**Acceptance:**
- The specified visitor flow does not require sign-in, an account, or authorization.
- The application includes only the three pages in REQ-001 and does not depend on the excluded external services or integrations.

**Evidence:** Work `674d9253-8ffe-468e-93c3-fb38b7c16298` (scope exclusions); `review:requirements` Artifact `2a04185d-3c75-40e4-9a84-6b145fb9e205`; `review:frontend` Artifact `b1c0b5b6-8811-4b21-9ff7-bce1b5637777`; `review:backend` Artifact `f41451e3-d1e1-4da9-a2d5-fd6962862e31`.

**Decision provenance:** Approved AFU Artifact `2a04185d-3c75-40e4-9a84-6b145fb9e205`; contributing subjects `AFU-REQ-003`, `AFU-RULE-001`.

**Supersedes:** None

## Observable contracts

### Visitor submission flow

1. A visitor opens Home and activates “Go to contact form,” arriving at Contact Form.
2. The visitor enters Name and Email Address. When they submit, each field is checked against REQ-003. Invalid values receive field-specific feedback beneath the affected field and are not sent as a valid submission.
3. A valid pair is submitted to the application backend. While the backend outcome is pending, the visitor is not shown Confirmation.
4. If the backend confirms successful storage, the visitor sees Confirmation with the submitted pair and personalized first-name greeting.
5. If the backend reports failure, the visitor remains on Contact Form and sees the exact message in REQ-007. The visitor can retry; because duplicate submissions are accepted, an ambiguous prior outcome may result in an additional stored pair.
6. “Back to home” returns to Home from both Contact Form and Confirmation.

### Stored-submission behavior

- Each correctly submitted pair accepted by the backend is stored as a pair.
- Identical submissions remain separate accepted submissions.
- Stored pairs have no time-based expiry or scheduled deletion.
- Request frequency or total-record count does not itself cause application-level rejection. Physical resource limits or service failures remain possible and follow the generic failure behavior.

No endpoint, transport, request/response schema, or protocol is established by this PRD; interface design belongs to a later phase.

## Acceptance

The product is acceptable when all of the following are demonstrated:

1. The three-page journey and return actions in REQ-001 work, with no additional page.
2. Page content, controls, and visual hierarchy match the supplied Figma evidence as required by REQ-002.
3. Required-field, length, email-format, boundary, and field-specific error behavior meets REQ-003.
4. Correct submissions are stored, duplicate pairs remain distinct, and records have no time-based expiry, as required by REQ-004 and REQ-005.
5. No product-level request-frequency or total-record cap rejects a valid submission (REQ-006).
6. Confirmation is shown only after successful storage, and backend failure stays on the form with the exact required message (REQ-007).
7. Confirmation displays the actual submitted values in the design treatment (REQ-008).
8. The visitor flow requires no authentication and introduces none of the excluded integrations or pages (REQ-009).

## Risks

- **Indefinite retention and unbounded volume:** The binding decisions require indefinite retention and no application-level request-frequency or total-record limit. Cumulative storage and processing demand therefore has no product-defined bound; finite physical capacity can eventually cause backend failure. This risk does not change the no-limit requirement, and genuine backend failures follow REQ-007.
- **Feasibility is unverified:** The reviewed snapshot for `https://github.com/demeedogg/backend-test-app.git`, `main@e32f25d9ddb0612877f778f00e2de22bf0e1107c`, contains only a README and provides no persistence, runtime, deployment, or capacity evidence (`analysis:backend-test-app-7cad18d3`). The reviewed snapshot for `https://github.com/demeedogg/frontend-test-app.git`, `main@858555bf61e4c27218013d1d542bce07745fc16d`, likewise contains only a README and no application behavior or integration evidence (`analysis:frontend-test-app-dfaf2284`). These findings do not establish infeasibility, but durable indefinite storage, operational capacity, external reachability, and deployed behavior are not verified by the supplied evidence.
- **Ambiguous failure and retry:** Storage may succeed even when the visitor does not observe the success response. The required failure presentation may then be followed by a retry that stores a duplicate. The product allows this outcome; the failure message does not guarantee absence of a stored pair.

The exact approved Requirements Review set is review round 1, set `1fe2ae0ba6622bcf9685c943af32a862dac6898d7116232cb007224612fb61a0`, approved by interaction `7c49b0de-630b-4c97-87ec-c82e520defa6`. Its three reviewed artifacts are requirements `2a04185d-3c75-40e4-9a84-6b145fb9e205`, frontend `b1c0b5b6-8811-4b21-9ff7-bce1b5637777`, and backend `f41451e3-d1e1-4da9-a2d5-fd6962862e31`. The approved reviews report no blocked questions.
