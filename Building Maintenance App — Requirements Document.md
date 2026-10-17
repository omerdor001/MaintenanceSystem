# Building Maintenance App — Requirements Document

Oct 16, 2026

## 1. Purpose and scope

The Building Maintenance App lets building employees report faults, book guest parking and events, and see building notices. It gives the building management and maintenance team one view of work orders, preventive maintenance, and regulatory certificates. It replaces manual phone and email requests.

The app covers six core capabilities:

1. Maintenance requests by category
2. Guest parking reservations
3. Preventive maintenance schedules
4. QR-code location scanning
5. Notices and announcements
6. Management dashboard and reports

The scope also includes certificate tracking for regulated equipment (elevators, fire safety, electrical panels, generators) and booking of event spaces and equipment.

## 2. Stakeholders and user roles

The app has four user roles. Names in the deck are sample data.

| Role | Who | Main needs |
| --- | --- | --- |
| Employee | Any person working in the building | Open and track own requests, reserve guest parking, book event spaces, read notices |
| Building manager | Manages the building and its notices | Publish notices, send SMS to staff, approve events, see all requests |
| Maintenance manager | Runs maintenance and vendors | See all requests, manage the preventive schedule, upload certificates, get urgent alerts |
| Technician / contractor | Carries out work orders | Receive assigned tasks, update status, attach before/after photos |

Each role sees only what it needs. Employees see only their own requests. Managers see all requests in the building and the preventive maintenance board.

## 3. Functional requirements

Each requirement has an ID and the deck slide where it is shown. The slide number is the source for the requirement.

### 3.1 Login and access (slide 3)

| ID | Requirement | Slide |
| --- | --- | --- |
| FR-01 | Users log in with employee number or organizational username, and password. | 3 |
| FR-02 | Optional single sign-on against the company Active Directory. | 3 |
| FR-03 | Users can reset a forgotten password. | 3 |
| FR-04 | Access is set by role. Employees see only their own requests; managers see all requests and the preventive maintenance board. | 3 |
| FR-05 | On first login, the user confirms their department and floor, used for fast request routing. | 3 |

### 3.2 Home screen and navigation (slide 4)

| ID | Requirement | Slide |
| --- | --- | --- |
| FR-06 | On every app open, a banner shows the latest notices. | 4 |
| FR-07 | Home has two large buttons: New request and My requests. | 4 |
| FR-08 | Home shows a personal summary of the user's requests by status: open, in progress, completed. | 4 |
| FR-09 | Bottom navigation has five tabs: Home, Requests, Scan, Updates, Profile. | 4 |

### 3.3 Opening a maintenance request (slides 5 and 6)

| ID | Requirement | Slide |
| --- | --- | --- |
| FR-10 | The user picks a category from icons: general maintenance, HVAC, electrical, plumbing, cleaning, elevators, guest parking, other. | 5 |
| FR-11 | Choosing a category opens the request form with the category filled in and locked. | 6 |
| FR-12 | The form has location, description, optional photo, and urgency (low, medium, high). | 6 |
| FR-13 | Choosing high urgency sends an immediate alert to the on-duty maintenance manager, in addition to the normal queue. | 6 |
| FR-14 | The request is assigned automatically to the responsible person for its category. The building manager can reassign it. | 6 |
| FR-15 | Guest parking is a separate flow, not a fault request. | 5 |

### 3.4 My requests and tracking (slide 7)

| ID | Requirement | Slide |
| --- | --- | --- |
| FR-16 | The request list has four tabs: All, Open, In progress, Completed. | 7 |
| FR-17 | Each request shows a colored status tag: red for open, orange for in progress, green for completed. | 7 |
| FR-18 | Opening a request shows its full timeline: who handled it, when, technician notes, and before and after photos if available. | 7 |

### 3.5 QR code location scanning (slides 6 and 8)

| ID | Requirement | Slide |
| --- | --- | --- |
| FR-19 | Scanning a QR sticker opens a new request with the location pre-filled. | 8 |
| FR-20 | Before the form opens, the app shows the identified location for confirmation. | 8 |
| FR-21 | QR stickers are placed in restrooms, kitchens, safe rooms, meeting rooms, and corridor junctions. | 8 |

### 3.6 Guest parking reservation (slide 9)

| ID | Requirement | Slide |
| --- | --- | --- |
| FR-22 | A day view shows guest parking slots as available, reserved, or taken. | 9 |
| FR-23 | The user reserves a slot with one tap, without coordinating manually. | 9 |
| FR-24 | Each reservation stores date, time range, guest name, vehicle number, and host employee. This data is used at the parking gate and for security checks. | 9 |
| FR-25 | Users see their active reservations on one screen and can cancel them until arrival time. | 9 |

### 3.7 Event and space booking (slides 10 and 11)

| ID | Requirement | Slide |
| --- | --- | --- |
| FR-26 | The event form captures name, location, date, time range, and expected number of attendees. | 10 |
| FR-27 | Only spaces free for the chosen date, time, and capacity are offered. Availability is checked against the space calendar. | 10 |
| FR-28 | After the basic details, the user selects equipment and sets an exact quantity per item with plus and minus controls (for example 15 chairs, 18 catering portions). | 11 |
| FR-29 | Quantities are passed to the operations team as part of the preparation task. | 11 |
| FR-30 | Before approval, the user can change quantities. After approval, a material change requires the maintenance manager to update the booking. | 11 |
| FR-31 | "My events" shows each request as pending approval, approved, or rejected. Requests can be edited or cancelled until the event date. | 10 |

### 3.8 SMS to staff (slide 12)

| ID | Requirement | Slide |
| --- | --- | --- |
| FR-32 | The building manager sends an SMS to all employees, to one department, or to one employee. | 12 |
| FR-33 | The message field shows a character counter against the 160-character limit. | 12 |
| FR-34 | Before sending, the screen shows the number of expected recipients, to catch sends that are too broad or too narrow. | 12 |

### 3.9 Preventive maintenance (slides 13 and 14)

| ID | Requirement | Slide |
| --- | --- | --- |
| FR-35 | Each building system has a schedule with a frequency: weekly, monthly, quarterly, or annual. | 14 |
| FR-36 | Tasks are generated automatically from each schedule. | 13 |
| FR-37 | Each task is assigned to a technician or vendor, with a target date. | 13 |
| FR-38 | Users get a reminder before the target date. Overdue tasks alert the maintenance manager. | 13 |
| FR-39 | The board shows the monthly completion percentage and a calendar of upcoming tasks. | 13 |
| FR-40 | The management screen lets the maintenance manager add and edit plans. Each plan shows system, frequency, owner or vendor, last done date, next due date, and status. | 14 |
| FR-41 | The system can produce a preventive maintenance compliance report for audits. | 13 |

### 3.10 Regulatory certificates and inspections (slides 16 to 18)

| ID | Requirement | Slide |
| --- | --- | --- |
| FR-42 | The list shows counts of valid, expiring within 30 days, and expired certificates. | 16 |
| FR-43 | A certificate record stores system, inspection type, inspecting body, inspection date, valid-until date, and a scanned file (PDF or image). | 17 |
| FR-44 | The reminder lead time is set per certificate, for example 30 days before expiry. | 17 |
| FR-45 | If a certificate is not renewed, reminders repeat, and their frequency increases close to expiry. | 18 |
| FR-46 | Expired certificates are shown in red and listed at the top of the dashboard until renewed. | 18 |
| FR-47 | Reminders go to the maintenance manager and an optional second contact, through the app and by email or SMS. | 18 |
| FR-48 | Uploaded certificate files can be viewed and downloaded at any time. | 17 |

### 3.11 Notices and announcements (slide 15)

| ID | Requirement | Slide |
| --- | --- | --- |
| FR-49 | A notices screen keeps the full history. The latest notices appear as a banner on Home. | 15 |
| FR-50 | Each notice is tagged as general notice, planned maintenance, or alert. | 15 |
| FR-51 | The building manager publishes notices, can target a floor or department, and sets an expiry date. | 15 |

### 3.12 Management dashboard and reports (slides 19 and 20)

| ID | Requirement | Slide |
| --- | --- | --- |
| FR-52 | The dashboard shows open requests, requests opened this month, average handling time, SLA compliance, and recent requests. | 19 |
| FR-53 | The dashboard shows requests by category for the last 30 days. | 19 |
| FR-54 | The dashboard shows a six-month trend of average handling time. | 20 |
| FR-55 | The dashboard shows monthly maintenance cost by category. | 20 |
| FR-56 | The dashboard shows average response time per technician or vendor. | 20 |
| FR-57 | The dashboard shows guest parking utilization, the number of overdue preventive plans, and total monthly maintenance cost. | 20 |

The figures in the deck (for example 37 requests opened, 94% SLA compliance) are mock-up data and are not requirements.

## 4. Non-functional requirements

The deck does not set most of these. The Status column shows whether a requirement comes from the deck or is proposed here for confirmation.

| ID | Area | Requirement | Status |
| --- | --- | --- | --- |
| NFR-01 | Language | The user interface is in Hebrew, right-to-left. | From deck |
| NFR-02 | Platforms | The app is a responsive website for phones, tablets, and desktops. The platforms to support are set: browsers only, with no native iOS or Android app. | Decided |
| NFR-03 | Security | Logins use the company identity system where available. Passwords and personal data are encrypted in transit and at rest. | Proposed |
| NFR-04 | Access control | Every screen and data query checks the user's role on the server, not only in the app. | Proposed |
| NFR-05 | Personal data | Guest names, vehicle numbers, and employee details are personal data. Collection, retention, and deletion must follow the applicable privacy law. Legal review is needed. | To confirm |
| NFR-06 | Audit trail | Every status change, assignment, reservation, and certificate upload is logged with user and time. | Proposed |
| NFR-07 | Notifications | Urgent alerts and certificate reminders are delivered within a few minutes of the triggering event. The target is to be set. | To confirm |
| NFR-08 | Availability | The app is available during building hours. The uptime target and maintenance window are to be set. | To confirm |
| NFR-09 | Integration | The app connects to the building management system for staff, parking, and calendar data. The integration method is to be set. | To confirm |
| NFR-10 | Reporting | Dashboard figures refresh at least daily. The refresh frequency is to be set. | To confirm |
| NFR-11 | Accessibility | Screens use high-contrast status colors and do not rely on color alone. The status tags also use text labels. | Proposed |
| NFR-12 | Data retention | Completed requests, reservations, and certificate files are kept for a period to be set by the building management and legal review. | To confirm |

## 5. Out of scope and open questions

The following are not in this version:

- Payments or billing for guest parking or event equipment.
- Vendor invoicing and contract management.
- Access control for doors or turnstiles. Parking data is shared with the gate, but the gate itself is not changed.
- Tenant or external visitor accounts. Only building staff log in.

Open questions for the next review:

- [ ] Launch platform: a responsive website for phones and desktop, with no native app.
- [ ] Who approves event bookings, and how are conflicts with other bookings resolved?
- [ ] Which external systems are the source of truth for staff directory, calendar, and parking data?
- [ ] Who receives SMS costs, and is there a monthly limit on SMS sends?
- [ ] What are the response and resolution targets (SLA) per urgency level?
- [ ] Does the SLA of 94% in the dashboard mock-up match an agreed target?
- [ ] What is the retention period for requests, certificates, and parking records?

## 6. Next steps

1. **Approve the screen design.** Review the example screens in the deck and collect a list of changes.
2. **Define categories and locations.** List the areas, systems, and request categories for the building in Caesarea.
3. **Plan QR sticker placement.** Map the points in the building for stickers and produce them.
4. **Develop and test.** Build the app, connect it to the management system, and test with a small group of employees.

The open questions in section 5 should be answered before step 4 begins.

## 7. Technical challenges

The app is a responsive website, so each challenge below is a browser challenge. Each row links to the requirement IDs in sections 3 and 4. Items marked with an owner need a decision before development.

| ID | Challenge | Why it is hard | Requirements | Proposed approach |
| --- | --- | --- | --- | --- |
| TC-01 | Responsive Hebrew layout | Right-to-left screens must work from a 360 px phone to a desktop. Wide tables (parking grid, certificates, dashboard) do not fit a phone. | FR-09, FR-16, FR-27, FR-42, FR-52, NFR-01, NFR-02 | Mobile-first responsive design with logical CSS properties for right-to-left. Tables become stacked cards on phones. Test on real devices. |
| TC-02 | QR scanning in a browser | Camera access needs HTTPS and user permission. iOS Safari and Android Chrome behave differently. | FR-19, FR-20, FR-21 | Browser-based QR scanning. Each sticker encodes a link with its location code. If the camera is refused, the user picks the location from a list. |
| TC-03 | Urgent alerts on the web | Browser push works on Android Chrome. On iOS it works only after the web app is added to the home screen. | FR-13, FR-38, FR-45, FR-47 | Web push where supported. Email and SMS are the fallback. Urgent alerts go by SMS as well as push. |
| TC-04 | Weak signal in basements and machine rooms | Technicians work in parking levels and machine rooms with poor signal. Lost uploads can cause duplicates or lost updates. | FR-12, FR-18, NFR-07, NFR-08 | Save changes on the device first and sync when the connection returns. Retry uploads. Make status updates safe to repeat. |
| TC-05 | Photos and certificate files | Phone photos are several MB each. Certificate scans need access control. | FR-12, FR-18, FR-43, FR-48 | Resize and compress photos in the browser before upload. Store files in private storage. Serve them through short-lived links after an access check. Limit file type and size. |
| TC-06 | Server-side role checks | Employees must not see other people's requests. Guest data must be limited to managers. Hiding a screen is not enough. | FR-04, FR-05, FR-24, NFR-04 | Check role and ownership on every server call. Write automated tests for each role. |
| TC-07 | Single sign-on | The company directory (Active Directory) must be reachable from the web app. Its setup depends on the company's IT team. | FR-01, FR-02, FR-05, NFR-03 | Use SAML or OpenID Connect through the company identity provider. Launch with password login and add SSO once the provider is confirmed. **Owner: company IT.** |
| TC-08 | Double booking | Two users may book the same parking slot or room at the same time. | FR-22, FR-23, FR-27, FR-30 | Enforce uniqueness in the database inside a transaction. Show a clear message when a slot was just taken. |
| TC-09 | Hebrew SMS length | Hebrew text is sent as UCS-2, so one SMS holds 70 characters, not 160. The deck counter (142/160) would be wrong, and Hebrew messages cost more. | FR-32, FR-33, FR-34 | Count characters the way the SMS gateway encodes them. Show the number of SMS parts and the estimated cost. **Owner: building manager, with the SMS provider.** |
| TC-10 | Work week and calendar | Israel's work week runs Sunday to Thursday. The deck shows days from Sunday (א' to ש'). Holidays change the schedule. | FR-27, FR-36, FR-38, FR-40 | Store dates in Israel time. Use a Sunday-to-Thursday week. Keep a holiday calendar that the building manager can edit. |
| TC-11 | Recurring task generation | Weekly, monthly, quarterly, and annual schedules must create each task once, even if a job runs twice or a run is missed. | FR-35, FR-36, FR-37 | Scheduled job that creates tasks for each due date. Each task has a unique key (schedule plus date), so reruns create no duplicates. Missed runs are caught up on the next run. |
| TC-12 | Reminder escalation | Reminders must repeat and speed up as a certificate nears expiry, and must stop once a new certificate is uploaded. | FR-44, FR-45, FR-46, FR-47 | Daily reminder job that calculates the next send date from the expiry date. A renewal cancels pending reminders at once. |
| TC-13 | Dashboard performance | The dashboard aggregates six months of requests, costs, and response times, and must load quickly on phones. | FR-52 to FR-57, NFR-10 | Precompute daily summaries. The dashboard reads summaries, not raw rows. Load the mobile view in small parts. |
| TC-14 | Audit trail and privacy | Every change must be logged. Guest and employee data must be deleted on schedule. | FR-24, NFR-05, NFR-06, NFR-12 | Append-only audit log. Retention rules run as scheduled jobs. Legal review before launch. **Owner: building management and legal.** |

Challenge TC-15 covers SMS sending, which affects staff messages and urgent alerts.

| ID | Challenge | Why it is hard | Requirements | Proposed approach |
| --- | --- | --- | --- | --- |
| TC-15 | SMS to staff and alerts | Hebrew messages are sent as UCS-2, so one SMS holds 70 characters and long messages split into several billed parts. The sender name must be registered with the provider. Department messages need phone numbers and department membership in the directory. Failed deliveries must be visible to the sender. | FR-13, FR-32, FR-33, FR-34, FR-47, NFR-07 | Choose a gateway that supports Hebrew and an Israeli sender name. Show SMS parts, estimated cost, and recipient count before sending. Track delivery per number, retry failures, log every send, and cap sends per day. **Owner: building manager, with the SMS provider and legal for opt-out and privacy rules.** |

Challenge TC-16 covers where files are saved and where the website is hosted.

| ID | Challenge | Why it is hard | Requirements | Proposed approach |
| --- | --- | --- | --- | --- |
| TC-16 | File storage and website hosting | Certificate scans, request photos, and before and after photos contain private data and must stay private. Storing them on the web server makes backup and restore hard. The hosting location affects privacy rules. Staff need the site during building hours, so hosting must be reliable and reachable from the office and from phones. | FR-12, FR-18, FR-43, FR-48, NFR-03, NFR-05, NFR-08, NFR-12 | Store records in a managed database and files in private cloud storage, not on the web server. Serve files through short-lived links after an access check. Encrypt at rest and in transit. Run daily backups and test a restore. Host the website on a managed platform with HTTPS and a company domain, with separate test and production environments. The hosting region is chosen with legal. If the company requires on-premises hosting, the same design runs on a company server. **Owner: company IT and building management.** |

Challenges TC-17 to TC-23 extend the list above.

| ID | Challenge | Why it is hard | Requirements | Proposed approach |
| --- | --- | --- | --- | --- |
| TC-17 | QR sticker location data | Each sticker must match one room or point in the building. Stickers get moved, damaged, or removed when rooms change, so the code-to-location list drifts. | FR-19, FR-20, FR-21 | Keep a location list in the admin screen, with one code per sticker. Show the location name on the scan confirmation. Use weatherproof print. Review the list each quarter. |
| TC-18 | Login and session security | Accounts are used on office computers and phones, and some devices are shared at reception. Password reset links can be abused. | FR-01, FR-03, FR-04, NFR-03 | Lock accounts after repeated failed logins. End sessions after inactivity. Make reset links expire quickly and work once. Log logins and failed attempts. Require a second factor for manager accounts. |
| TC-19 | Equipment quantities and operations handoff | Approved quantities must reach the operations team exactly, and later changes must reach them too. The requested quantity may not be in stock. | FR-28, FR-29, FR-30 | Store each quantity line with a version number. Send an update to the operations task on every change. Show stock limits if operations provides them. **Owner: operations, to confirm the stock data source.** |
| TC-20 | Gate, directory, and calendar integration | Guest parking data must reach the gate system. Staff, department, and room calendar data come from other systems that may be slow or down. | FR-22, FR-23, FR-27, NFR-09 | Confirm interfaces with the gate and directory vendors before development. Sync on a schedule and keep the last good copy. Show a warning when data is stale. **Owner: company IT and the gate vendor.** |
| TC-21 | Accessibility in Hebrew | Screens must meet WCAG 2.1 AA. That needs enough contrast, keyboard use, screen reader labels, and a right-to-left reading order. Status colors must not be the only signal. | NFR-01, NFR-11, FR-17 | Test contrast and screen reader output with Hebrew text. Pair every status color with a text label. Check focus order on the right-to-left layout. Run an accessibility check in each release. |
| TC-22 | Cost and SLA data | The dashboard needs maintenance costs by category and SLA figures, but the SLA definition and cost source are not set. Vendor invoicing is out of scope, so costs must come from another source. | FR-52, FR-55, FR-56, NFR-10 | Define SLA as a rule in working hours, Sunday to Thursday, agreed with the owner. Take costs from an external finance export. Label each dashboard figure with its source and date. **Owner: finance and building management.** |
| TC-23 | Slow mobile networks | Pages must load quickly on phones in basements and on weak signal, especially photo uploads and the dashboard. | NFR-02, FR-18, FR-52 | Keep the first screen light. Load images and charts after the main content. Compress photos before upload. Test on a throttled mobile connection. The load time target is to be set. |
