# Design description: Artifact's Repo test

## Render inventory
- `render-confirmation-page-2-241` — Confirmation page; successful submission summary and return action.
- `render-contact-form-page-2-200` — Contact form page; populated fields with an invalid-email state.
- `render-home-page-2-169` — Home page; introduction and contact-form call to action.

## Renders
### render-confirmation-page-2-241: Confirmation page
**Purpose:** Reassure the visitor that their contact details were submitted and show the submitted pair (`render-confirmation-page-2-241`).

**Visible content and structure:**
- A white header places the Details mark and name on the left, with Home and Contact navigation on the right; Contact is highlighted (`render-confirmation-page-2-241`).
- A centered white card on a pale background groups a check icon, the heading “You’re all set!”, and the message “Your contact details were submitted successfully. Thanks for getting in touch, Alex.” (`render-confirmation-page-2-241`).
- A shaded summary within the card labels the example values Name “Alex Morgan” and Email “alex.morgan@example.com” (`render-confirmation-page-2-241`).
- The footer repeats “© 2026 Details” and “A little information. A simple connection.” at opposite sides (`render-confirmation-page-2-241`).

**Controls and user actions:**
- “Back to home” is the card’s prominent outlined action; the work specifies that it returns to the Home page (`render-confirmation-page-2-241`).

**Connections:**
- The work specifies that a successful form submission leads from `render-contact-form-page-2-200` to this confirmation screen, and that “Back to home” returns to `render-home-page-2-169`.

### render-contact-form-page-2-200: Contact form page
**Purpose:** Collect the visitor’s name and email address (`render-contact-form-page-2-200`).

**Visible content and structure:**
- The shared header has the Details brand at left and Home and Contact links at right, with Contact highlighted (`render-contact-form-page-2-200`).
- Above the main card is an arrow and “Back to home” link (`render-contact-form-page-2-200`). The card begins with a contact icon, “Your contact details”, the sentence “Add your name and email below to get in touch.”, and the note “Both fields are required.” (`render-contact-form-page-2-200`).
- The form shows labeled Name and Email fields. The example Name value is “Alex Morgan”; the example Email value is the malformed “alex.morgan@” (`render-contact-form-page-2-200`).
- The footer area below the card includes a lock icon and “Your details stay private and secure.” The page footer repeats the copyright and connection slogan (`render-contact-form-page-2-200`).

**Controls and user actions:**
- “Submit details” is the full-width primary form action (`render-contact-form-page-2-200`). The work specifies that it submits the form to the backend and that the confirmation screen appears only after a successful response.
- The “Back to home” link is a return action; the work also specifies a return-to-home action on the confirmation screen (`render-contact-form-page-2-200`, `render-confirmation-page-2-241`).

**States and feedback:**
- The render shows an invalid-email state: the Email field has red error styling and an alert icon, with the message “Enter a valid email address, like alex@example.com.” below it (`render-contact-form-page-2-200`). The work requires both fields, a 1–100 character name, and a valid email of at most 254 characters, with field-specific errors below invalid fields.
- No name-error or empty-fields error state is shown in this render. The work specifies that on backend failure the visitor remains on this form and sees “Unable to submit your information. Please try again.”

**Connections:**
- The work specifies that the home-page “Go to contact form” action leads from `render-home-page-2-169` to this page, and that successful submission leads to `render-confirmation-page-2-241`.

### render-home-page-2-169: Home page
**Purpose:** Introduce the contact-details flow and direct the visitor to its form (`render-home-page-2-169`).

**Visible content and structure:**
- The Details mark and name appear in the left side of the header; Home and Contact navigation sit at right, with Home highlighted (`render-home-page-2-169`).
- A centered white panel contains a contact icon, the heading “Let’s get in touch.”, and the description “Share your name and email using our contact form. Just the essentials, all in one place.” (`render-home-page-2-169`).
- Beneath the primary action is the reassurance “Only two fields. Less than a minute.” A lock icon and “Your details stay private and secure.” sit below the panel (`render-home-page-2-169`).
- The page footer repeats “© 2026 Details” and “A little information. A simple connection.” (`render-home-page-2-169`).

**Controls and user actions:**
- The full-width green “Go to contact form” button includes a right arrow. The work specifies that it opens the contact form (`render-home-page-2-169`).

**Connections:**
- The work establishes the transition from this home screen to `render-contact-form-page-2-200` through “Go to contact form”.

## Shared patterns
- All three renders use the Details brand in a white top navigation bar, a pale neutral page background, dark headings, muted supporting text, and deep green accents (`render-home-page-2-169`, `render-contact-form-page-2-200`, `render-confirmation-page-2-241`).
- The header provides Home and Contact navigation, with the current section highlighted in each render (`render-home-page-2-169`, `render-contact-form-page-2-200`, `render-confirmation-page-2-241`).
- All three renders share the “© 2026 Details” and “A little information. A simple connection.” footer copy (`render-home-page-2-169`, `render-contact-form-page-2-200`, `render-confirmation-page-2-241`).

## Open questions
- The confirmation render uses the sample name “Alex Morgan”, email “alex.morgan@example.com”, and message ending “Thanks for getting in touch, Alex.” (`render-confirmation-page-2-241`). The work does not say whether to replace the sample name and email with the actual submitted values while preserving the message and styling.
- Only an invalid-email example is rendered; name validation and empty-field feedback are not visually specified (`render-contact-form-page-2-200`). The work supplies the required-field and length rules, but not exact error copy for those cases.
