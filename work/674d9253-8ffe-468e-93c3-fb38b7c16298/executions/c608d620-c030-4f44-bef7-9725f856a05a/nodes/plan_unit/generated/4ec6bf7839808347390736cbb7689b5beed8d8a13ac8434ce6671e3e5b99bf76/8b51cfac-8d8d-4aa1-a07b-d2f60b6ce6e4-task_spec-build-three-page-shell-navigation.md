---
task_id: build-three-page-shell-navigation
depends_on: []
complexity: medium
complexity_reason: The empty starter requires a complete client entry point and route structure while preserving the shared design across three page surfaces; navigation regressions, premature Confirmation exposure, or image coupling to an unavailable service would break the unit's acceptance.
implementation_constraints:
  - Work only in https://github.com/demeedogg/frontend-test-app.git at the assigned main destination, planned from commit 858555bf61e4c27218013d1d542bce07745fc16d.
  - Provide exactly the Home, Contact Form, and Confirmation page surfaces, with the specified Home-to-Contact action and return/navigation actions; do not add authentication, external integrations, or other pages.
  - Follow the Details branding, page content, shared header/footer treatment, and visual hierarchy evidenced by the supplied design renders.
  - Keep form validation/submission behavior and Confirmation content and success-only transition in the frontend submission-flow Delivery unit; this Task establishes the shared shell and navigation integration seam only.
references:
  requirement_ids:
    - REQ-001
    - REQ-002
    - REQ-009
  design_references:
    - render-home-page-2-169
    - render-contact-form-page-2-200
    - render-confirmation-page-2-241
  openapi_operations: []
---

# Task: Build the three-page Details shell and Home/contact navigation

## Requirements satisfied

- REQ-001 — Establish the three-page client structure, Home-to-Contact Form action, Home/Contact header navigation, and Contact Form return-to-Home action. Keep Confirmation inaccessible until the successful-submission flow supplies a success result.
- REQ-002 — Implement the shared Details header/footer and Figma-aligned Home screen, and carry the shared visual treatment through Contact Form and the internal Confirmation shell scaffold.
- REQ-009 — Keep the visitor experience anonymous and self-contained, with no extra page or external integration.

## Outcome

The empty frontend destination becomes an independently runnable client application with a Figma-aligned Home page, the shared Details page shell, and a three-page structure ready for the sibling submission-flow work. Visitors can navigate from Home to Contact Form and back using the Home call to action, header navigation, and Contact Form “Back to home” action. The Confirmation shell is prepared for later successful-submission rendering but cannot be reached from the Home or Contact navigation or by directly opening its path without successful-submission state.

## Behavioral contract

- Home is the default page and presents the Details header, Home-active navigation, centered introductory panel, “Let’s get in touch.” heading, supporting copy, “Go to contact form” action with its arrow treatment, “Only two fields. Less than a minute.” reassurance, privacy reassurance, and shared footer.
- Activating “Go to contact form” or the header Contact link opens Contact Form. The header Home link and Contact Form “Back to home” action return to Home. The active header section follows the current page: Home on Home and Contact on Contact Form and Confirmation.
- Contact Form uses the shared header, page background, content alignment, and footer; retain a content slot for the form behavior owned by the submission-flow unit. Do not implement form validation, backend calls, or submission outcomes here.
- Provide an internal Confirmation page shell using the shared header/footer and Figma-aligned page container. Do not add Confirmation content or expose this view through navigation or a direct route absent successful-submission state; the submission-flow unit owns the success transition and confirmation content.
- Keep routing within exactly the three named page surfaces. Unknown paths must not render a new branded or product page.
- Document the selected dependency/runtime versions and local verification and image-build commands. Do not depend on another application or service to serve the frontend.

## Implementation approach

1. Use React 19 with TypeScript and Vite for the client, React Router 7 with browser-history routes for `/`, `/contact`, and `/confirmation`, npm with a committed lockfile, Vitest and React Testing Library for focused client tests, and a multi-stage image with an unprivileged Nginx static runtime. These are the simplest conventional defaults for the empty standalone frontend; document exact dependency versions, the Node.js 22 LTS build-stage patch, and the exact unprivileged Nginx image release tag rather than using floating `latest` tags. The pinned frontend snapshot contains only a README, so no existing behavior or technology compatibility needs preservation.
2. Implement reusable Details branding, header/navigation, page background/content frame, footer, and small local icon treatments needed by the cited renders. Match the Home render's copy, control hierarchy, green primary action, pale neutral background, centered white panel, and shared footer. Use local code or assets; do not add external APIs or services.
3. Create the Home, Contact Form, and Confirmation page surfaces with clear route/component boundaries. Wire Home and Contact navigation and the Contact Form return action. Keep Confirmation behind transient in-memory successful-submission state: redirect to Home if `/confirmation` is opened without that state; the submission-flow unit owns producing the state and rendering Confirmation content.
4. Add focused client tests for Home-to-Contact navigation, Home/Contact header navigation, Contact Form return-to-Home, active navigation treatment, exactly-three-page routing, and the Confirmation access guard. Add a local visual comparison or deterministic render check for Home and shared shell at the supplied design's desktop reference size; use reasonable responsive layout defaults where the design does not specify breakpoints.
5. Add repository-local build-context exclusions and the standalone, version-pinned, non-root Nginx runtime image. Configure the static server to serve the built client and fall back to the application entry for the three client routes. Build the image successfully without starting a container or requiring the backend/another service, then replace the frontend repository root `build-manifest.json` with the built image name and tag in the documented format.

## Acceptance criteria

- Home shows the Details brand, Home-active header navigation, “Let’s get in touch.” and “Share your name and email using our contact form. Just the essentials, all in one place.”, the “Go to contact form” action with arrow, “Only two fields. Less than a minute.”, privacy reassurance, and the shared “© 2026 Details” / “A little information. A simple connection.” footer.
- Selecting the Home call to action or Contact header link reaches Contact Form. Selecting Home from Contact Form or its “Back to home” action returns to Home. The active header item is correct on Home and Contact Form.
- The Contact Form surface includes its shared shell and a content slot for the independently owned submission flow; its form validation and submission are not implemented in this Task.
- The client has only the Home, Contact Form, and Confirmation page surfaces. No additional page is rendered for an unknown path; Confirmation is not exposed from navigation or a direct path without the successful-submission state needed by the later flow.
- Home and shared shell match the hierarchy, copy, colors, and spacing treatment of `render-home-page-2-169`, `render-contact-form-page-2-200`, and `render-confirmation-page-2-241` at the supplied desktop reference size. The Contact render's form-specific field/error behavior and Confirmation's success content remain for their owning unit.
- The application has no authentication or external service/integration dependency and runs/builds without access to the backend.
- Focused client tests pass. The standalone runtime image builds successfully without starting a container, uses a version-pinned base/runtime and a non-root runtime user, and the committed root `build-manifest.json` records that image's name and tag.

## Verification

- Run the documented repository-native client test command and confirm navigation, active-section state, three-page routing, unknown-path behavior, and the Confirmation access guard.
- Run the documented local production build and the Home/shared-shell visual check against the cited renders. These checks must not start or require the backend.
- Build the repository-local frontend runtime image from its documented command without starting a container. Confirm that the image configuration runs as a non-root user and that build-context exclusions do not remove files needed by the application.
- Inspect the root `build-manifest.json` after the successful image build and verify it contains the exact image name and tag built by this Task.
