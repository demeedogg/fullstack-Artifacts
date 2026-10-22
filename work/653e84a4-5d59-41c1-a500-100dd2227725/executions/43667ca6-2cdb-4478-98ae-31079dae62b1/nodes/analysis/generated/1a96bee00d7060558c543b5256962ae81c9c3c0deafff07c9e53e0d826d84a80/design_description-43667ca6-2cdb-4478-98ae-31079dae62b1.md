# Design description: TASK MANAGMENT (retry)

The Figma file contains annotated cover/style material, an early wireframe set, high-fidelity screens, fully populated Design Area screens with revised sample data, and a second Design Area set of skeleton/loading views. The screen descriptions below separate these render groups; repeated renders are called out rather than treated as new behavior. The design shows a task-learning dashboard for a signed-in learner, but its sample data and visible controls do not specify the access rules or task-review lifecycle in the written requirements.

## Render inventory
- `render-label-2-197` — Label; ancillary label frame.
- `render-label-2-204` — Label; ancillary label frame.
- `render-cover-2-211` — Cover; Task Management dashboard and responsive-design title slide.
- `render-license-2-1762` — License; usage terms slide.
- `render-icon-general-2-2646` — Icon/General; icon library overview.
- `render-color-style-2-46689` — Color Style; color palette reference.
- `render-button-2-47116` — Button; button variants and states reference.
- `render-content-2-47744` — Content; desktop/mobile settings and activity component examples.
- `render-typography-2-48216` — Typography; type scale and weights reference.
- `render-web---dashboard-84-2544` — Web - Dashboard; low-fidelity desktop dashboard.
- `render-mobile---dashboard-84-2820` — Mobile - Dashboard; low-fidelity mobile dashboard.
- `render-web---task-90-3615` — Web - Task; low-fidelity task listing.
- `render-mobile---task-94-2936` — Mobile - Task; low-fidelity task listing.
- `render-web---detail-task-95-3635` — Web - Detail Task; low-fidelity task detail and submission panel.
- `render-mobile---detail-task-95-3773` — Mobile - Detail Task; low-fidelity task detail and submission panel.
- `render-web---mentors-98-2847` — Web - Mentors; low-fidelity mentor directory.
- `render-mobile---mentors-98-3058` — Mobile - Mentors; low-fidelity mentor directory.
- `render-web---message-98-3220` — Web - Message; low-fidelity inbox and conversation.
- `render-mobile---message-98-3415` — Mobile - Message; low-fidelity inbox.
- `render-mobile---message---chat-98-3524` — Mobile - Message - Chat; low-fidelity conversation.
- `render-web---settings---general-98-3576` — Web - Settings - General; low-fidelity general preferences.
- `render-mobile---settings---general-98-3660` — Mobile - Settings - General; low-fidelity general preferences.
- `render-web---settings---notification-98-3703` — Web - Settings - Notification; low-fidelity notification preferences.
- `render-mobile---settings---notification-98-3789` — Mobile - Settings - Notification; low-fidelity notification preferences.
- `render-web---dashboard-6-2335` — Web - Dashboard; high-fidelity desktop dashboard.
- `render-mobile---dashboard-36-3066` — Mobile - Dashboard; high-fidelity mobile dashboard.
- `render-web---task-36-3071` — Web - Task; high-fidelity task listing.
- `render-mobile---task-36-4048` — Mobile - Task; high-fidelity task listing.
- `render-web---detail-task-39-1865` — Web - Detail Task; high-fidelity task detail and submission panel.
- `render-mobile---detail-task-84-2102` — Mobile - Detail Task; high-fidelity task detail and submission panel.
- `render-web---mentors-36-5489` — Web - Mentors; high-fidelity mentor directory.
- `render-mobile---mentors-36-6747` — Mobile - Mentors; high-fidelity mentor directory.
- `render-web---message-38-2152` — Web - Message; high-fidelity inbox and conversation.
- `render-mobile---message-53-2129` — Mobile - Message; high-fidelity inbox.
- `render-mobile---message---chat-53-2749` — Mobile - Message - Chat; high-fidelity conversation.
- `render-web---settings---general-53-3034` — Web - Settings - General; high-fidelity general preferences.
- `render-mobile---settings---general-55-2018` — Mobile - Settings - General; high-fidelity general preferences.
- `render-web---settings---notification-58-2195` — Web - Settings - Notification; high-fidelity notification preferences.
- `render-mobile---settings---notification-58-2279` — Mobile - Settings - Notification; high-fidelity notification preferences.
- `render-web---dashboard-133-4811` — Web - Dashboard; Design Area dashboard render.
- `render-mobile---dashboard-133-5084` — Mobile - Dashboard; Design Area mobile dashboard render.
- `render-web---task-133-5269` — Web - Task; Design Area task-list render.
- `render-mobile---task-133-5523` — Mobile - Task; Design Area mobile task-list render.
- `render-web---detail-task-133-5729` — Web - Detail Task; Design Area task-detail render.
- `render-mobile---detail-task-133-5867` — Mobile - Detail Task; Design Area mobile task-detail render.
- `render-web---mentors-133-5960` — Web - Mentors; Design Area mentor-directory render.
- `render-mobile---mentors-133-6171` — Mobile - Mentors; Design Area mobile mentor-directory render.
- `render-web---message-133-6333` — Web - Message; Design Area inbox and conversation render.
- `render-mobile---message-133-6534` — Mobile - Message; Design Area mobile inbox render.
- `render-mobile---message---chat-133-6643` — Mobile - Message - Chat; Design Area mobile conversation render.
- `render-web---settings---general-133-6695` — Web - Settings - General; Design Area general-settings render.
- `render-mobile---settings---general-133-6779` — Mobile - Settings - General; Design Area mobile general-settings render.
- `render-web---settings---notification-133-6822` — Web - Settings - Notification; Design Area notification-settings render.
- `render-mobile---settings---notification-133-6908` — Mobile - Settings - Notification; Design Area mobile notification-settings render.
- `render-web---dashboard-133-7928` — Web - Dashboard; desktop skeleton/loading state.
- `render-mobile---dashboard-133-8172` — Mobile - Dashboard; mobile skeleton/loading state.
- `render-web---task-133-8347` — Web - Task; desktop skeleton/loading state.
- `render-mobile---task-133-8564` — Mobile - Task; mobile skeleton/loading state.
- `render-web---detail-task-133-8634` — Web - Detail Task; desktop skeleton/loading state.
- `render-mobile---detail-task-133-8745` — Mobile - Detail Task; mobile skeleton/loading state.
- `render-web---mentors-133-8818` — Web - Mentors; desktop skeleton/loading state.
- `render-mobile---mentors-133-9084` — Mobile - Mentors; mobile skeleton/loading state.
- `render-web---message-133-9252` — Web - Message; desktop inbox/chat skeleton/loading state.
- `render-mobile---message-133-9411` — Mobile - Message; mobile inbox skeleton/loading state.
- `render-mobile---message---chat-133-9501` — Mobile - Message - Chat; mobile chat skeleton/loading state.
- `render-web---settings---general-133-9539` — Web - Settings - General; desktop skeleton/loading state.
- `render-mobile---settings---general-133-9616` — Mobile - Settings - General; mobile skeleton/loading state.
- `render-web---settings---notification-133-9660` — Web - Settings - Notification; desktop skeleton/loading state.
- `render-mobile---settings---notification-133-9739` — Mobile - Settings - Notification; mobile skeleton/loading state.

## Renders
### render-label-2-197: Label
**Purpose:** Ancillary frame label, not a learner-facing screen.

### render-label-2-204: Label
**Purpose:** Ancillary frame label, not a learner-facing screen.

### render-cover-2-211: Cover
**Purpose:** Introduces a responsive Task Management dashboard design and advertises a multi-screen UI kit. It does not specify product behavior.

### render-license-2-1762: License
**Purpose:** Describes the source design kit's use terms. It permits personal/commercial project use and disallows reselling the kit or using it in a paid UI kit; this is file-level licensing material, not an in-app screen.

### render-icon-general-2-2646: Icon/General
**Purpose:** Reference sheet of categorized icons. It is visual source material, not product content.

### render-color-style-2-46689: Color Style
**Purpose:** Shows named primary, success, error, warning, information, and secondary color ramps for the visual system.

### render-button-2-47116: Button
**Purpose:** Shows primary, secondary, and minimal button variants in small, medium, and large sizes, with enabled, hover, pressed, focused, and disabled examples. These are component states rather than specified business states.

### render-content-2-47744: Content
**Purpose:** Shows desktop and responsive arrangements for settings controls and the dashboard activity/running-task widgets. It supports layout comparison but does not add task rules.

### render-typography-2-48216: Typography
**Purpose:** Shows regular, medium, semibold, and bold text scales as visual reference.

### render-web---dashboard-84-2544: Web - Dashboard
**Purpose:** Summarizes learner activity and highlights mentors, upcoming tasks, a date selector, and a selected task.

**Visible content and structure:** The desktop shell has a left navigation rail, a central greeting and activity area, and a right-hand calendar and “Task Today” panel. A “Running Task” count/percentage and weekly activity chart sit above mentor and upcoming-task cards. The selected task panel shows a progress bar, time estimate, numbered detail list, and “Go To Detail” button.

**Controls and user actions:** Sidebar entries are Overview, Task, Mentors, Message, and Settings. The chart has a “This Week” selector; calendar and carousel arrows are visible. “Go To Detail” labels a button, but its destination is not proven by this render alone.

### render-mobile---dashboard-84-2820: Mobile - Dashboard
**Purpose:** Presents the dashboard as a vertically stacked mobile page.

**Visible content and structure:** A compact top bar places menu, notification, and profile icons above the greeting, running-task summary, activity chart, mentor/task cards, calendar, and selected-task details. The screen retains the desktop dashboard's content groups in a single column.

**Controls and user actions:** The menu, bell, profile, chart interval, carousel arrows, calendar arrows, overflow menu, and “Go To Detail” button are visible. The render does not show their resulting screens or interactions.

### render-web---task-90-3615: Web - Task
**Purpose:** Lets a learner browse the task catalog/list.

**Visible content and structure:** A desktop navigation rail accompanies “Explore Task,” a task search field, category and “Sort By: Deadline” controls, and horizontal card groups titled “Time Limit” and “New Task.” Cards show an image, title, discipline, progress percentage/bar, time or days remaining, and small avatar stacks.

**Controls and user actions:** Search, category, sort, and carousel arrows are visible. The list does not label the task lifecycle stages from the requirements.

### render-mobile---task-94-2936: Mobile - Task
**Purpose:** Shows the task catalog/list in a mobile layout.

**Visible content and structure:** “Explore Task,” search, and a filter icon precede vertically stacked task cards grouped under “Time Limit” and “New Task.” Each card includes an image, discipline, progress bar, time/deadline hint, and avatar stack.

**Controls and user actions:** Menu, bell, profile, search, filter, and section arrows are visible. Filtering and task-card destinations are not demonstrated.

### render-web---detail-task-95-3635: Web - Detail Task
**Purpose:** Presents a task description and a learner submission area.

**Visible content and structure:** A large video/image player, title, categories, “Get Mentors” link, student-involvement and duration metadata, description, and assessment checklist occupy the main column. A separate “Assigned Assignments” panel shows a student name/class/number, “Last Modified,” a “File submissions” drop area, and “Submit” button.

**Controls and user actions:** Media controls, “Get Mentors,” drag-or-browse file selection, and “Submit” are visible. The panel is labeled for an assigned student, but this render does not specify who may open it or whether the student can edit after completion. No review status, correction reason, version history, or mentor evaluation action is shown.

### render-mobile---detail-task-95-3773: Mobile - Detail Task
**Purpose:** Reflows the task detail and file-submission flow for mobile.

**Visible content and structure:** The player, task information, description, and assessment checklist appear first; “Assigned Assignments,” student details, last-modified date, upload area, and “Submit” appear below in a separate card.

**Controls and user actions:** The file drop/browse area and “Submit” remain visible. Role rules, submission versions, review states, and feedback are not depicted.

### render-web---mentors-98-2847: Web - Mentors
**Purpose:** Lets a learner browse mentor profiles.

**Visible content and structure:** “Explore Mentors” with search, category and popular-sort controls sits above “Recent Mentors” and a larger “Mentors” grid. Profile cards show name, specialty, bio, task count, review score, and “+ Follow” or “Followed.”

**Controls and user actions:** Search, category, sort, carousel arrows, and follow labels are visible. The directory does not show a way to inspect other students' tasks; it also does not identify assigned mentors.

### render-mobile---mentors-98-3058: Mobile - Mentors
**Purpose:** Shows the mentor directory as a one-column mobile list.

**Visible content and structure:** Search/filter controls and a “Recent Mentors” card precede profile cards with names, specialties, summaries, task counts, and ratings.

**Controls and user actions:** Menu, bell, profile, search, filter, carousel arrows, and follow states are visible. No assignment relationship or student-task access is shown.

### render-web---message-98-3220: Web - Message
**Purpose:** Combines a conversation list and an open conversation.

**Visible content and structure:** The left pane has “Search Name” and rows with participant avatar, name, latest-message snippet, time, and red-dot or blue-check indicators. The right pane has the selected contact and online indicator, date divider, sent/received text and image messages, timestamps, and a composer with attachment and send controls.

**Controls and user actions:** Search, video/phone icons, message input, attachment, and send are visible. The red dots and check marks distinguish row states visually, but their exact read/delivery semantics are not defined. A separate top-bar bell is present.

### render-mobile---message-98-3415: Mobile - Message
**Purpose:** Shows the message inbox on mobile.

**Visible content and structure:** Search and a single-column conversation list show names, latest snippets, relative times, and red-dot or blue-check marks. The top bar has menu, bell, and profile icons.

**Controls and user actions:** Search and conversation rows are visible. The open-chat view is a separate render, `render-mobile---message---chat-98-3524`; no transition is explicitly demonstrated.

### render-mobile---message---chat-98-3524: Mobile - Message - Chat
**Purpose:** Shows one mobile conversation.

**Visible content and structure:** A contact header with online state and video/phone icons precedes alternating message bubbles, including an image attachment, date/time labels, and a bottom composer with attachment and send controls.

**Controls and user actions:** Back, video, phone, composer, attachment, and send icons are visible. The render does not specify notification-read behavior or conversation authorization.

### render-web---settings---general-98-3576: Web - Settings - General
**Purpose:** Provides general account/display preferences.

**Visible content and structure:** “General” and “Notification” tabs lead a settings panel with a Language dropdown showing “English (Default),” a Timezone dropdown also showing “English (Default),” and 24/12-hour choices under a second “Timezone” label, followed by “Save Changes.”

**Controls and user actions:** Tab labels, dropdowns, radio-style choices, and “Save Changes” are visible. The “English (Default)” value in the Timezone dropdown and the repeated “Timezone” label above the 24/12-hour choice make the intended values/label unclear.

### render-mobile---settings---general-98-3660: Mobile - Settings - General
**Purpose:** Reflows general preferences for mobile.

**Visible content and structure:** General/Notification tabs sit above a single-column settings card with a Language dropdown, a Timezone dropdown, 24/12-hour choices under another “Timezone” label, and a full-width “Save Changes” button.

**Controls and user actions:** Dropdowns, radio-style choices, and save are visible. As in `render-web---settings---general-98-3576`, the Timezone dropdown's “English (Default)” value and the repeated label above 24/12-hour choices are ambiguous.

### render-web---settings---notification-98-3703: Web - Settings - Notification
**Purpose:** Lets a user configure notification preferences.

**Visible content and structure:** The Notification tab lists switches for Message, Task Update, Task Deadline, and Mentor Help, followed by “Save Changes.” Message and Task Deadline appear enabled; Task Update and Mentor Help appear disabled.

**Controls and user actions:** Switches and save are visible. The page does not say whether these preferences apply to email, in-app notifications, or both.

### render-mobile---settings---notification-98-3789: Mobile - Settings - Notification
**Purpose:** Shows notification preferences in the mobile layout.

**Visible content and structure:** Four labeled switches—Message, Task Update, Task Deadline, and Mentor Help—are in a settings card with a full-width “Save Changes” button. Message and Task Deadline appear enabled.

**Controls and user actions:** Switches and save are visible; channel scope and behavior after saving are not shown.

### render-web---dashboard-6-2335: Web - Dashboard
**Purpose:** High-fidelity desktop view of learner progress and shortcuts.

**Visible content and structure:** The DNX shell has a persistent left navigation and a greeting. “Running Task” shows 65, a 45% ring, and 100 tasks; an “Activity” chart is set to “This Week.” “Monthly Mentors” cards show follow state, task count, and rating. “Upcoming Task” cards show progress and days left. The right column combines a July 2022 calendar with “Task Today,” a progress slider, duration, avatar stack, numbered “Detail Task” list, and “Go To Detail.” A help-center card remains in the lower navigation rail.

**Controls and user actions:** Navigation, notification bell with red badge, weekly selector, carousel/calendar arrows, follow affordances, overflow menu, progress slider, and “Go To Detail” are visible. The chart, ring, and card progress are not explained as equivalent completion measures.

### render-mobile---dashboard-36-3066: Mobile - Dashboard
**Purpose:** High-fidelity mobile dashboard.

**Visible content and structure:** The desktop content is stacked vertically: greeting, running-task summary and chart, a single monthly-mentor card, upcoming-task card, calendar, and the “Task Today” detail card. The calendar and selected task are lower on the page than the dashboard summary.

**Controls and user actions:** Menu, bell with badge, profile, chart-period selector, carousel/calendar arrows, overflow menu, progress slider, and “Go To Detail” are visible. The render establishes a mobile arrangement, not behavior parity.

### render-web---task-36-3071: Web - Task
**Purpose:** High-fidelity task catalog/list.

**Visible content and structure:** “Explore Task” has search, Category, and “Sort By: Deadline” controls. “Time Limit” and “New Task” each contain horizontal cards with imagery, title, discipline, progress percentage/bar, time remaining, and avatar stacks.

**Controls and user actions:** Search, category, sort, and carousel arrows are visible. “Time Limit” and “New Task” are the shown group labels; no states corresponding to in review, needs correction, or completed are named.

### render-mobile---task-36-4048: Mobile - Task
**Purpose:** High-fidelity mobile task catalog/list.

**Visible content and structure:** The search field and filter icon lead into full-width image cards under “Time Limit” and “New Task,” with progress, duration/deadline hint, and avatars.

**Controls and user actions:** Menu, bell, profile, search, filter, and carousel arrows are visible. This layout does not show category/sort labels or the results of changing filters.

### render-web---detail-task-39-1865: Web - Detail Task
**Purpose:** High-fidelity task information and learner submission view.

**Visible content and structure:** The main area contains a media player, task title/category, “Get Mentors,” student count, duration, description, and an “Essence of Assessment” checklist. The right “Assigned Assignments” card identifies a student and class, shows a last-modified date, and offers a dashed “File submissions” upload region and “Submit.”

**Controls and user actions:** Media controls, “Get Mentors,” file drop/browse, and “Submit” are visible. The checklist is shown with checked icons, but they are not explained as task-completion status. There is no visible review/return/approve control, correction-reason field, late indicator, or prior-submission/version list.

### render-mobile---detail-task-84-2102: Mobile - Detail Task
**Purpose:** High-fidelity mobile task detail and submission view.

**Visible content and structure:** Media, task metadata, description, and checked assessment items form the upper card; task/student details and file upload form the lower card.

**Controls and user actions:** “Get Mentors,” file drop/browse, and “Submit” are visible. The mobile render keeps the same submission capability, but does not show lifecycle feedback or version history.

### render-web---mentors-36-5489: Web - Mentors
**Purpose:** High-fidelity mentor discovery and profile browsing.

**Visible content and structure:** Recent mentor cards appear above a multi-column directory. Profile cards show avatar, name, specialty, short biography, task count, review score, and Follow/Followed state. Search, category, and “Sort By: Popular” controls sit above.

**Controls and user actions:** Search, category, sort, carousel arrows, and follow controls are visible. Profiles are presented as a directory; no student task details or assigned-student relationship is shown.

### render-mobile---mentors-36-6747: Mobile - Mentors
**Purpose:** High-fidelity mobile mentor directory.

**Visible content and structure:** A recent-mentor card and stacked directory cards retain profile summaries, specialty, task counts, ratings, and follow states.

**Controls and user actions:** Menu, bell, profile, search, filter, carousel arrows, and follow controls are visible. No task access for other students is represented.

### render-web---message-38-2152: Web - Message
**Purpose:** High-fidelity desktop inbox and conversation view.

**Visible content and structure:** Conversation rows include participant, latest snippet, relative time, and either a red dot or blue double-check. The selected chat shows a contact's online state, text/image messages, timestamps, and a composer. A global notification bell is separate from the conversation list.

**Controls and user actions:** Search, video/phone, attachment, text-entry, and send controls are visible. The adjacent notification and message indicators are visually separate; the screen does not define whether reading one affects the other.

### render-mobile---message-53-2129: Mobile - Message
**Purpose:** High-fidelity mobile inbox.

**Visible content and structure:** Search and vertically stacked conversations show avatar, name, latest message, relative time, red unread-looking dot, or blue sent/read-looking checks.

**Controls and user actions:** Menu, bell with badge, profile, search, and conversation rows are visible. Chat is rendered separately in `render-mobile---message---chat-53-2749`; no route transition is explicitly evidenced.

### render-mobile---message---chat-53-2749: Mobile - Message - Chat
**Purpose:** High-fidelity mobile conversation.

**Visible content and structure:** The contact header displays an online indicator and video/phone controls. The thread has a date marker, sent/received bubbles, an image attachment, timestamps, and a bottom composer with attachment and send icons.

**Controls and user actions:** Back, video, phone, attachment, text entry, and send are visible. No task-linked conversation context or message-read setting appears.

### render-web---settings---general-53-3034: Web - Settings - General
**Purpose:** High-fidelity desktop general preferences.

**Visible content and structure:** General and Notification tabs; a Language dropdown showing “English (Default)”; a Timezone dropdown also showing “English (Default)”; 24 Hours/12 Hours choices under a second “Timezone” label; and “Save Changes.”

**Controls and user actions:** Tabs, dropdowns, radio-style choices, and save are visible. The Timezone dropdown's displayed value and the repeated label above the time-format choices remain ambiguous.

### render-mobile---settings---general-55-2018: Mobile - Settings - General
**Purpose:** High-fidelity mobile general preferences.

**Visible content and structure:** General and Notification tabs above a spacious preferences card with Language and Timezone dropdowns, 24/12-hour choices under another “Timezone” label, and a bottom save button.

**Controls and user actions:** Dropdowns, radio-style choices, and save are visible. The Timezone dropdown's “English (Default)” value and time-format label remain unclear.

### render-web---settings---notification-58-2195: Web - Settings - Notification
**Purpose:** High-fidelity desktop notification preference settings.

**Visible content and structure:** Four switches are labeled Message, Task Update, Task Deadline, and Mentor Help. Message and Task Deadline are shown on; Task Update and Mentor Help are off. “Save Changes” sits below.

**Controls and user actions:** Switches and save are visible. No channel label distinguishes email preferences from in-app notification behavior.

### render-mobile---settings---notification-58-2279: Mobile - Settings - Notification
**Purpose:** High-fidelity mobile notification preferences.

**Visible content and structure:** The same four notification categories and shown on/off states are arranged vertically, with a full-width “Save Changes” button.

**Controls and user actions:** Switches and save are visible; channel scope and any saved/failed feedback are not depicted.

### render-web---dashboard-133-4811: Web - Dashboard
**Purpose:** Populated Design Area variant of the desktop dashboard.

**Visible content and structure:** Greeting, running-task and activity metrics, mentor and upcoming-task card rows, calendar, selected-task detail, and help card use the same broad arrangement as `render-web---dashboard-6-2335`. This variant changes visible sample data, including the product wordmark/name, learner, and displayed calendar date.

**Controls and user actions:** Navigation, chart/calendar arrows, notification bell, and detail CTA are visible. No distinct transition or business state is demonstrated.

### render-mobile---dashboard-133-5084: Mobile - Dashboard
**Purpose:** Populated Design Area variant of the mobile dashboard.

**Visible content and structure:** Greeting, metrics, chart, mentor/task cards, calendar, and selected-task detail follow the same vertical flow as `render-mobile---dashboard-36-3066`, with changed sample learner/date details.

**Controls and user actions:** Menu, bell, profile, carousels, calendar, and detail CTA recur without new behavior.

### render-web---task-133-5269: Web - Task
**Purpose:** Populated Design Area variant of the desktop task catalog.

**Visible content and structure:** Search/category/deadline-sort controls and “Time Limit”/“New Task” card carousels show task imagery, titles, progress, estimated time, and avatars, following the same structure as `render-web---task-36-3071`.

**Controls and user actions:** Search, category, sort, and arrows are visible; no additional lifecycle states are represented.

### render-mobile---task-133-5523: Mobile - Task
**Purpose:** Populated Design Area variant of the mobile task catalog.

**Visible content and structure:** Mobile search/filter header and stacked task cards grouped by “Time Limit” and “New Task” follow the same pattern as `render-mobile---task-36-4048`.

**Controls and user actions:** Menu, bell, profile, search, filter, and arrows recur; their resulting states are not shown.

### render-web---detail-task-133-5729: Web - Detail Task
**Purpose:** Populated Design Area variant of the desktop detail/submission view.

**Visible content and structure:** Player, task information, assessment checklist, assigned-student metadata, upload zone, and Submit button follow the same structure as `render-web---detail-task-39-1865`; the student name and last-modified date differ.

**Controls and user actions:** Upload and Submit remain the only visible submission actions; review decisions, version selection, and correction feedback are absent.

### render-mobile---detail-task-133-5867: Mobile - Detail Task
**Purpose:** Populated Design Area variant of the mobile detail/submission view.

**Visible content and structure:** Task information and checklist precede a separate assigned-assignment/student/file-submission card, following the same mobile arrangement as `render-mobile---detail-task-84-2102`; sample student/date information differs.

**Controls and user actions:** The upload area and Submit action recur. No visible review or lifecycle feedback is added.

### render-web---mentors-133-5960: Web - Mentors
**Purpose:** Populated Design Area variant of the desktop mentor directory.

**Visible content and structure:** Recent mentors and profile cards show biographies, specialties, follow status, task counts, and review ratings.

**Controls and user actions:** Search/category/popularity sorting, carousel arrows, and Follow recur; no assignment filter is visible.

### render-mobile---mentors-133-6171: Mobile - Mentors
**Purpose:** Populated Design Area variant of the mobile mentor directory.

**Visible content and structure:** Recent mentor and stacked profile cards repeat on mobile.

**Controls and user actions:** Search/filter, arrows, and Follow recur; no student-task access is represented.

### render-web---message-133-6333: Web - Message
**Purpose:** Populated Design Area variant of the desktop inbox/chat.

**Visible content and structure:** Conversation list and selected thread repeat the unread-looking dots, check marks, contact state, messages, attachments, and composer.

**Controls and user actions:** Search, call/video, attach, and send recur. The relationship between notification state and conversation-read state remains unspecified.

### render-mobile---message-133-6534: Mobile - Message
**Purpose:** Populated Design Area variant of the mobile inbox.

**Visible content and structure:** Search and stacked conversations with snippets, relative times, red dots, and blue checks repeat.

**Controls and user actions:** Menu, bell, profile, search, and conversation rows recur; no distinct state is shown.

### render-mobile---message---chat-133-6643: Mobile - Message - Chat
**Purpose:** Populated Design Area variant of the mobile conversation.

**Visible content and structure:** Contact header, online indicator, conversation bubbles, image message, timestamps, and composer repeat.

**Controls and user actions:** Back, video/phone, attachment, and send recur without added business behavior.

### render-web---settings---general-133-6695: Web - Settings - General
**Purpose:** Populated Design Area variant of desktop general settings.

**Visible content and structure:** Language/Timezone dropdowns, 24/12-hour choices, General/Notification tabs, and Save Changes repeat.

**Controls and user actions:** The Timezone dropdown's English value and repeated label above time-format choices remain unresolved.

### render-mobile---settings---general-133-6779: Mobile - Settings - General
**Purpose:** Populated Design Area variant of mobile general settings.

**Visible content and structure:** The mobile preferences card and General/Notification tabs repeat.

**Controls and user actions:** Dropdowns, time-format options, and Save Changes recur; the Timezone dropdown's displayed value and time-format label remain unclear.

### render-web---settings---notification-133-6822: Web - Settings - Notification
**Purpose:** Populated Design Area variant of desktop notification settings.

**Visible content and structure:** Message and Task Deadline appear on; Task Update and Mentor Help appear off; Save Changes is shown.

**Controls and user actions:** The switch categories recur without showing email-versus-in-app scope or feedback.

### render-mobile---settings---notification-133-6908: Mobile - Settings - Notification
**Purpose:** Populated Design Area variant of mobile notification settings.

**Visible content and structure:** The same four switch categories, shown on/off states, and Save Changes button recur.

**Controls and user actions:** No channel distinction or save result is shown.

### render-web---dashboard-133-7928: Web - Dashboard
**Purpose:** Desktop dashboard skeleton/loading state.

**Visible content and structure:** The desktop shell keeps the dashboard's activity chart and running-task card, mentor/task rows, calendar, and selected-task panel, but most labels and content are represented by placeholder bars and shapes. This is a distinct loading/placeholder render rather than a populated dashboard.

### render-mobile---dashboard-133-8172: Mobile - Dashboard
**Purpose:** Mobile dashboard skeleton/loading state.

**Visible content and structure:** The mobile dashboard's top bar, metric/chart area, mentor and task cards, calendar, and task detail appear as stacked placeholders; the chart includes a visible “2 Task” tooltip.

### render-web---task-133-8347: Web - Task
**Purpose:** Desktop task-list skeleton/loading state.

**Visible content and structure:** The “Explore Task” shell, search/category/sort positions, “Time Limit” and “New Task” sections, and multi-card arrangement remain, while images and card text are placeholders.

### render-mobile---task-133-8564: Mobile - Task
**Purpose:** Mobile task-list skeleton/loading state.

**Visible content and structure:** The mobile “Explore Task” header, search/filter row, “Time Limit” and “New Task” headings, and stacked cards remain as a loading layout with placeholder image/text/progress areas.

### render-web---detail-task-133-8634: Web - Detail Task
**Purpose:** Desktop task-detail skeleton/loading state.

**Visible content and structure:** A large media placeholder with player controls, task-description/checklist placeholders, and a right-side assignment panel with student-detail placeholders and dashed upload area preserve the detail-page structure.

**Controls and user actions:** File selection and Submit remain visible; the render adds no review-state or version behavior.

### render-mobile---detail-task-133-8745: Mobile - Detail Task
**Purpose:** Mobile task-detail skeleton/loading state.

**Visible content and structure:** A media placeholder, task text/checklist placeholders, and a lower assignment/submission card with a dashed file area preserve the mobile detail-page structure.

**Controls and user actions:** File selection and Submit remain visible; review and feedback are not represented.

### render-web---mentors-133-8818: Web - Mentors
**Purpose:** Desktop mentor-directory skeleton/loading state.

**Visible content and structure:** The “Recent Mentors” carousel and multi-column mentor directory remain as profile-card placeholders, including avatar, text, and metadata regions.

### render-mobile---mentors-133-9084: Mobile - Mentors
**Purpose:** Mobile mentor-directory skeleton/loading state.

**Visible content and structure:** The recent-mentor card and vertically stacked profile cards use avatar and text placeholders.

### render-web---message-133-9252: Web - Message
**Purpose:** Desktop inbox/chat skeleton/loading state.

**Visible content and structure:** The conversation list and selected-chat pane remain in a two-column layout, with placeholder rows, contact header, message bubbles/media, and composer regions.

### render-mobile---message-133-9411: Mobile - Message
**Purpose:** Mobile inbox skeleton/loading state.

**Visible content and structure:** Search and conversation rows are represented by a vertical list of avatar and text placeholders.

### render-mobile---message---chat-133-9501: Mobile - Message - Chat
**Purpose:** Mobile chat skeleton/loading state.

**Visible content and structure:** The contact header, alternating message placeholders, large media placeholder, and bottom composer preserve the chat layout.

### render-web---settings---general-133-9539: Web - Settings - General
**Purpose:** Desktop general-settings skeleton/loading state.

**Visible content and structure:** Settings tabs, two dropdown-like fields, time-format choice controls, and save button are placeholder shapes; this loading render does not clarify the duplicate Timezone label in the populated variant.

### render-mobile---settings---general-133-9616: Mobile - Settings - General
**Purpose:** Mobile general-settings skeleton/loading state.

**Visible content and structure:** The mobile settings title, tabs, two dropdown-like fields, time-format options, and save button are represented by placeholders.

### render-web---settings---notification-133-9660: Web - Settings - Notification
**Purpose:** Desktop notification-settings skeleton/loading state.

**Visible content and structure:** Notification tabs, four switch-like controls, and a save button remain as placeholder shapes; category names and channel behavior are not visible in this loading state.

### render-mobile---settings---notification-133-9739: Mobile - Settings - Notification
**Purpose:** Mobile notification-settings skeleton/loading state.

**Visible content and structure:** The mobile notification tab, four switch-like controls, and save button are represented by placeholders; category names and channel behavior are not visible in this loading state.

## Shared patterns
- Across the dashboard, task, mentor, message, and settings screens, the desktop layout uses a persistent left navigation rail, top-right notification/profile affordances, pale neutral surfaces, dark text, and a vivid blue primary accent (`render-web---dashboard-6-2335`, `render-web---task-36-3071`, `render-web---detail-task-39-1865`, `render-web---mentors-36-5489`, `render-web---message-38-2152`, `render-web---settings---general-53-3034`).
- Mobile screens use a compact top bar with menu, notification, and profile icons, then stack the corresponding content vertically. The task detail, dashboard, and mentor list retain their principal content groups in mobile renders (`render-mobile---dashboard-36-3066`, `render-mobile---task-36-4048`, `render-mobile---detail-task-84-2102`, `render-mobile---mentors-36-6747`).
- Visible progress is represented with percentages and bars/rings in task cards and the dashboard, while task-detail checkmarks appear beside assessment items. The design does not define how these signals map to business completion (`render-web---dashboard-6-2335`, `render-web---task-36-3071`, `render-web---detail-task-39-1865`).
- Notification access appears as a bell with a red badge on several shells, while inbox rows separately show red dots and blue check marks; the file does not define their relationship (`render-web---dashboard-6-2335`, `render-web---message-38-2152`, `render-mobile---message-53-2129`).
- The UI uses English labels and sample dates/data; the requested product description is in Italian. The settings screen shows a Language preference but does not show Italian as a selected value (`render-web---settings---general-53-3034`, `render-mobile---settings---general-55-2018`).
- The second Design Area set provides structurally representative skeleton/loading views for dashboard, task, detail, mentor, messaging, and settings screens, but no loading completion, error, or empty-state feedback is shown (`render-web---dashboard-133-7928`, `render-web---task-133-8347`, `render-web---detail-task-133-8634`, `render-web---mentors-133-8818`, `render-web---message-133-9252`, `render-web---settings---notification-133-9660`).

## Open questions
- The dashboard and task catalog use task counts, percentages, progress bars, and “Time Limit”/“New Task” headings, but do not label the required lifecycle states. Which visible status should correspond to not started, in progress, in review, needs correction, and completed, and how should review and correction feedback appear? Relevant renders: `render-web---dashboard-6-2335`, `render-web---task-36-3071`, `render-web---detail-task-39-1865`, `render-mobile---detail-task-84-2102`.
- The task detail shows a file upload and Submit action but no explicit submission version list, due-date outcome, late marker, mentor review action, decision reason, or result/error feedback. Where should the learner and assigned mentor see version-specific submission and review states, including a stale-version decision? Relevant renders: `render-web---detail-task-39-1865`, `render-mobile---detail-task-84-2102`.
- The detail page includes an “Assigned Assignments” card with a student name and class, while the task catalog offers task cards and a mentor link. Which role is represented by these task/detail renders, and what should the UI show or block for direct access to another student's task? Relevant renders: `render-web---task-36-3071`, `render-web---detail-task-39-1865`, `render-web---mentors-36-5489`.
- Mentor directory cards expose “+ Follow”/“Followed,” but the requirements discuss mentor assignment and communication, not following. Is following required product behavior, and should a learner be able to message any listed mentor or only an assigned mentor? Relevant renders: `render-web---mentors-36-5489`, `render-mobile---mentors-36-6747`, `render-web---message-38-2152`.
- Notification settings identify categories but not channels; the global bell and inbox have separate indicators, with no notification list or read action shown. Are the switches for email only, and where are in-app notifications listed and marked read independently from conversations? Relevant renders: `render-web---settings---notification-58-2195`, `render-mobile---settings---notification-58-2279`, `render-web---message-38-2152`.
- The General settings screen shows “English (Default)” in the Timezone dropdown and labels the 24/12-hour choice “Timezone” as well. What timezone values and time-format label are intended? Relevant renders: `render-web---settings---general-53-3034`, `render-mobile---settings---general-55-2018`.
- Populated dashboard renders vary in wordmark, learner name, and displayed date across desktop/mobile and Design Area variants. Which wordmark and sample-state variant should guide the final screen copy/data? Relevant renders: `render-web---dashboard-6-2335`, `render-mobile---dashboard-36-3066`, `render-web---dashboard-133-4811`, `render-mobile---dashboard-133-5084`.
- The dashboard chart has a “This Week” filter and a calendar, but the file does not show how filtering affects the matching task lists or summary metrics. Which lists/indicators share date and filter ranges? Relevant renders: `render-web---dashboard-6-2335`, `render-mobile---dashboard-36-3066`.
- The design uses English copy and sample dates, and provides a Language setting without showing localized screens. Which language(s) and date/time conventions should be represented in the shipped desktop and mobile views? Relevant renders: `render-web---settings---general-53-3034`, `render-mobile---settings---general-55-2018`, `render-web---dashboard-6-2335`.
