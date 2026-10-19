# Delivery plan

## Build the designed page shell and navigation (`frontend-page-shell-and-navigation`)

- Type: `frontend`
- Depends on: None
- Repositories: `https://github.com/demeedogg/frontend-test-app.git` (branch: `main`)

Implement the shared Details header and footer, Figma-aligned Home landing screen, and the three-page client page structure with the Home-to-Contact Form action, Contact/Home navigation, and the form's Back to home action. Match the shared visual treatment evidenced by designReference render-home-page-2-169, render-contact-form-page-2-200, and render-confirmation-page-2-241; the Confirmation content and success-only transition are completed by the submission-flow unit. Satisfies the shell and navigation scope of REQ-001, REQ-002, and REQ-009. The frontend repository is an empty starter, so this first feature-bearing unit also establishes its standalone, version-pinned non-root runtime image and build-context exclusions, documenting the simplest conventional technology defaults selected. Completion is demonstrated by client tests showing the Home/form navigation and return actions work, no additional page is exposed, and the Home/shared shell matches the cited renders; its image builds without access to the backend or another network service.

### Tasks

- `build-three-page-shell-navigation`
  - Depends on: None
  - Artifact: `49201476-cc2f-4db7-9331-ebe826a129e0`

## Accept and persist valid contact submissions (`backend-contact-submission-and-persistence`)

- Type: `backend`
- Depends on: None
- Repositories: `https://github.com/demeedogg/backend-test-app.git` (branch: `main`)

Implement the backend submission capability for anonymous Name/Email pairs: enforce the required, 1–100 character Name and valid, at-most-254 character Email constraints; persist every accepted pair, including identical repeats; retain records without expiry or scheduled deletion; and impose no product-level request-frequency or total-record cap. A successful response must mean persistence succeeded, while a genuine processing or storage failure is reported as failure. Covers REQ-003, REQ-004, REQ-005, REQ-006, REQ-007, and the no-authentication/no-external-integration backend boundary in REQ-009. The pinned backend snapshot contains no runtime, API contract, or persistence technology, so choose and document the simplest conventional internal submission contract, runtime, and persistence defaults; do not add external integrations. This first feature-bearing unit also adds the backend repository's standalone, version-pinned non-root runtime image, startup configuration, build-context exclusions, and local image-build documentation. Completion is demonstrated by server-side tests for validation boundaries, persistence, duplicate acceptance, and truthful success/failure outcomes, plus a successful image build that does not require the frontend or a running database/service.

### Tasks

- `implement-contact-submission-persistence`
  - Depends on: None
  - Artifact: `dc130f9e-5bdd-4cb8-ae27-9f52579e5d45`

## Complete the validated submission and confirmation flow (`frontend-validated-submission-and-confirmation`)

- Type: `frontend`
- Depends on: `frontend-page-shell-and-navigation`, `backend-contact-submission-and-persistence`
- Repositories: `https://github.com/demeedogg/frontend-test-app.git` (branch: `main`)

Implement client-side Name and Email validation with field-specific errors below invalid fields, including the Figma invalid-email message and styling; submit valid values using the internal contract delivered by backend-contact-submission-and-persistence; remain on the form with the exact required failure message after an unsuccessful response; and show Confirmation only after success, with the actual submitted pair and personalized first-name greeting. Preserve the form and confirmation visual treatment and Confirmation-to-Home return action. Cite designReference render-contact-form-page-2-200 for form, validation, and failure states and render-confirmation-page-2-241 for the success transition, summary, and return action. Covers REQ-001, REQ-002, REQ-003, REQ-007, REQ-008, and REQ-009. No separate API specification is supplied, so consume the minimal internal contract established by the backend prerequisite; do not implement server logic or add pages/integrations. Completion is demonstrated by client tests using controlled success/failure responses for validation, pending/success/failure routing, exact failure copy, submitted-value rendering, and retry behavior; preserve the independently buildable frontend image established by the preceding frontend unit.

### Tasks

- `implement-validated-contact-submission-confirmation`
  - Depends on: None
  - Artifact: `e61374f8-7c68-43b9-8904-0528c6238f04`

## Compose and verify the complete contact journey (`contact-application-runtime-and-browser-verification`)

- Type: `test`
- Depends on: `frontend-page-shell-and-navigation`, `backend-contact-submission-and-persistence`, `frontend-validated-submission-and-confirmation`
- Repositories: `https://github.com/demeedogg/frontend-test-app.git` (branch: `main`), `https://github.com/demeedogg/backend-test-app.git` (branch: `main`)

In the Backend Repository, compose the independently packaged frontend and backend candidates with their required runtime dependency and exercise the complete application in a browser; correct only defects reproduced through that runtime in either application repository. Verify every user-observable requirement REQ-001 through REQ-009: exactly the three designed pages and navigation, Figma content/styling, required and boundary validation, below-field errors, successful storage and acceptance of repeated pairs, no application-level frequency/record cap, success-only Confirmation with actual submitted values, exact failure feedback with retry, and the absence of authentication or excluded integrations. Cover designReference render-home-page-2-169, render-contact-form-page-2-200, and render-confirmation-page-2-241, including Home-to-form, form-to-confirmation on success, and return-to-home transitions; exercise only the submission operation through the browser workflows, with no invented API operation identifier. Completion requires the composed runtime to start, the assigned browser workflows and storage outcomes to pass, any reproduced defects and required image manifests to be committed in the application repositories, and the composition to be stopped and cleaned.

### Tasks

- `compose-and-verify-contact-journey`
  - Depends on: None
  - Artifact: `ff76bed7-c88f-44c9-b8ba-97c821b1bd9d`
