# INIT_PROMPT: Building Maintenance App

You are building a mobile-first web application for the maintenance of one residential building in Caesarea (Kesariya), Israel. This file is your complete brief. Read it fully before you write any code.

---

## 1. Operating rules (apply to every step)

1. **Read the requirements first.** The full requirements are in `docs/requirements.md`. Requirement IDs (FR-xx, NFR-xx, TC-xx) are binding. Do not add features that have no requirement ID. If something is missing, ask.
2. **Confirm before every step.** Before you start any step, show the plan and wait for an explicit "confirm" from the user. The plan must list: files to create or change, database tables and policies, tests to write, and open questions. Do not begin coding until the user confirms.
3. **Validate after every step.** When a step is finished, run the validation checklist for that step (section 5). Write the result to `docs/validation/step-NN.md`. Then stop and ask the user to confirm before the next step.
4. **Stop on failure.** If any test, type check, lint, or build fails, fix it before reporting. Do not move on with a failing check. If you cannot fix it, report the failure and ask.
5. **Never skip the test for a requirement.** Each requirement listed in a step must have at least one automated test, named with its ID, for example `FR-04: employee sees only own requests`.
6. **Hebrew, right-to-left, mobile-first.** All user-facing text is in Hebrew. Layouts are right-to-left. Design for a 360 px phone first, then scale up to desktop.
7. **Personal data.** Guest names, vehicle numbers, and employee details are personal data (NFR-05). Do not log them, do not put them in test fixtures that look real, and do not expose them to roles that do not need them.
8. **Keep documentation current.** Update `docs/system.md` and `docs/building.md` whenever a step changes the system or the building data model.

---

## 2. Stack

- **Framework:** Next.js with TypeScript, using the App Router.
- **Styling:** Tailwind CSS, with logical properties for right-to-left layout.
- **Database, authentication, and file storage:** Supabase (PostgreSQL, Auth, Storage). Row-level security is enabled on every table.
- **Hosting:** Vercel, with a preview deployment for every step.
- **Testing:** Vitest for unit and integration tests. Playwright for end-to-end tests on a mobile viewport (360 px). A pgTAP or SQL test file for the row-level security policies.
- **Scheduled jobs:** Vercel Cron for reminders, task generation, and the daily summary.
- **SMS and email:** A gateway adapter with a fake implementation for tests.

If the user chooses a different stack before step 1, update this section and `docs/system.md` first, then confirm.

---

## 3. Roles (FR-04)

| Role | Can do |
| --- | --- |
| Employee | Open and track own requests. Reserve guest parking. Book event spaces. Read notices. |
| Building manager | Everything an employee can do, plus publish notices, send SMS, approve events, see all requests, and assign requests. |
| Maintenance manager | See all requests. Manage the preventive maintenance plan. Upload and track certificates. Receive urgent alerts. |
| Technician | See assigned requests only. Update status, add notes, and attach before and after photos. |

Permissions are enforced on the server through row-level security and server checks, not only in the interface (NFR-04). Every role has its own tests.

---

## 4. Documentation you must create

Create these files in the first step and keep them current.

- **`CLAUDE.md`** (repository root): stack, commands for test and local run, Hebrew and right-to-left rules, the four roles, and the rule that every step is confirmed before it starts.
- **`docs/requirements.md`**: the full requirements document. Copy it from the file the user provides.
- **`docs/system.md`**: the system description. Include the architecture (one codebase, one database, with each area as a module), the list of modules and the requirement IDs each one owns, the data model with tables and relationships, the roles and permission matrix, the integrations (SSO, SMS gateway, gate system, directory, calendar, finance export), the scheduled jobs and their schedules, and the decisions taken, with dates.
- **`docs/building.md`**: the building description. Use this template and fill in what the user provides. Mark unknown values as `TO CONFIRM` and never invent them.

  ```
  # Building description

  ## Location and identity
  - Name / address: TO CONFIRM
  - Number of floors: TO CONFIRM
  - Number of residential or office units: TO CONFIRM
  - Building manager: TO CONFIRM (role, not personal data)

  ## Physical spaces
  - Floors and their uses: TO CONFIRM
  - Restrooms, kitchens, safe rooms, meeting rooms, corridor junctions (QR sticker points, FR-21): TO CONFIRM
  - Event spaces and their capacities (FR-26, FR-27): TO CONFIRM
  - Guest parking: number of slots and levels (FR-22): TO CONFIRM
  - Machine room, generator room, electrical rooms: TO CONFIRM

  ## Building systems (for preventive maintenance and certificates)
  - Elevators: count, service company, inspection body: TO CONFIRM
  - Fire safety systems: TO CONFIRM
  - Electrical panels: TO CONFIRM
  - Generators: TO CONFIRM
  - Air conditioning and HVAC: TO CONFIRM
  - Plumbing and water: TO CONFIRM

  ## Request categories (FR-10)
  General maintenance, HVAC, electrical, plumbing, cleaning, elevators, guest parking, other.

  ## Responsible persons by category (FR-14)
  - Category -> responsible role (not personal data): TO CONFIRM

  ## Operating hours and calendar
  - Working week: Sunday to Thursday (TC-10)
  - Holidays calendar owner: TO CONFIRM
  - Building access hours: TO CONFIRM

  ## Vendors and external parties
  - Elevator service, fire, electrical, HVAC, cleaning: TO CONFIRM (company name and role only)
  ```

- **`docs/validation/step-NN.md`**: one file per step, written at the end of the step (section 5).

---

## 5. Validation checklist (run after every step)

After each step, complete all of the following and record the results in `docs/validation/step-NN.md`:

1. All automated tests for the step pass, and each requirement ID listed in the step has at least one test.
2. Type check, lint, and production build all pass.
3. Row-level security tests pass for every table touched in the step.
4. The step's "Done when" condition is demonstrated. Record it with a screenshot taken on a 360 px viewport.
5. The Hebrew text is correct and the layout is right-to-left on the 360 px viewport.
6. No personal data appears in logs or in test fixtures.
7. `docs/system.md` and `docs/building.md` are updated where relevant.
8. A preview deployment is available on Vercel.
9. A short summary: what was built, what was tested, what is open, and what the next step needs.

Then ask: **"Step NN is complete and validated. Confirm to start Step NN+1?"** and wait.

---

## 6. Before step 1: prerequisites

Do not start step 1 until the user has answered at least these open questions. Ask them as a list, and wait for the answers.

1. Launch platform: responsive website only (confirmed in the requirements), or is a native app needed later?
2. Hosting region: must personal data stay in Israel? (NFR-05)
3. Company identity provider for SSO: which system, and can IT provide a test account? (TC-07)
4. SMS gateway provider and sender name. (TC-09)
5. Gate system vendor and interface. (TC-20)
6. Stock data source for equipment. (TC-19)
7. SLA definition and cost source for the dashboard. (TC-22)
8. Data retention periods for requests, certificates, and parking records. (NFR-12)
9. Who approves event bookings? (FR-27 and section 5 of the requirements)

After the answers, fill `docs/building.md`, write `docs/system.md` with the decisions, and ask for confirmation to start step 1.

---

## 7. Build steps

Each step below is one working session. Start every step with the confirmation described in rule 2 of section 1.

### Step 1: Project skeleton
- **Scope:** Create the Next.js project, Tailwind setup, Supabase local environment, Vercel preview, `CLAUDE.md`, and the mobile-first shell with five bottom tabs: Home, Requests, Scan, Updates, Profile.
- **Requirements:** FR-09, NFR-01, NFR-02.
- **Tests:** The shell renders at 360 px. The five tabs are present and in Hebrew. The layout is right-to-left.
- **Done when:** The empty app runs on a phone in Hebrew, with a working preview URL.

### Step 2: Foundation (login, roles, audit log)
- **Scope:** Login with Supabase Auth. Roles table. Row-level security on all tables. First-login profile (department and floor). Audit log table with triggers for status and assignment changes. SSO is added only when IT confirms the provider (TC-07).
- **Requirements:** FR-01 to FR-05, NFR-03, NFR-04, NFR-06, TC-18.
- **Tests:** FR-01 login with valid and invalid credentials. FR-03 password reset. FR-04 role permission tests for all four roles. FR-05 first-login profile is required before use. NFR-06 an audit row is written on each change. TC-18 account lockout after repeated failures.
- **Done when:** The role test suite passes for every role, and the audit log records a test change.

### Step 3: Maintenance requests
- **Scope:** Home screen with quick actions and summary (FR-06 to FR-08). Category picker (FR-10). Request form with locked category, location, description, optional photo, and urgency (FR-11, FR-12). Automatic assignment by category (FR-14). "My requests" with four tabs and colored status tags (FR-16, FR-17). Status timeline with notes and photos (FR-18). Photo compression in the browser and private storage (TC-05). Urgent alerts use a logging stub until step 6 (FR-13).
- **Requirements:** FR-06 to FR-18, FR-13 (stub only), TC-04, TC-05.
- **Tests:** An employee sees only own requests. A technician sees only assigned requests. A request moves from open to in progress to completed. Photos are compressed before upload and stored privately. The offline queue retries a failed status update without creating duplicates (TC-04).
- **Done when:** A request moves from open to completed with photos, and the timeline shows each change.

### Step 4: QR location
- **Scope:** Location table with one code per sticker. Admin list of locations. Route `/scan/[code]` that opens a request with the location pre-filled. Camera scanning in the browser with a manual location fallback when the camera is refused (FR-19 to FR-21, TC-02, TC-17).
- **Requirements:** FR-19, FR-20, FR-21, TC-02, TC-17.
- **Tests:** An unknown code shows an error and no request. A known code shows the location for confirmation before the form opens. The manual fallback works when camera permission is denied.
- **Done when:** A sticker opens a request with the room already filled in, on a phone.

### Step 5: Notices
- **Scope:** Publish notices with targeting by floor or department, expiry date, and a tag (general, planned maintenance, alert). Notice history screen. Home banner shows the latest active notices (FR-49 to FR-51, FR-06).
- **Requirements:** FR-49, FR-50, FR-51, FR-06.
- **Tests:** Only the building manager can publish. Targeting shows a notice only to the selected floor or department. An expired notice disappears from the banner but stays in history.
- **Done when:** An expired notice is gone from the home banner and still visible in history.

### Step 6: Notifications
- **Scope:** Gateway adapter for SMS and email with a fake implementation for tests. Hebrew segment counting (UCS-2, 70 characters per segment) and cost display. Recipient preview (FR-34). Delivery log per number. Retries for failed sends. Urgent alerts replace the step 3 stub. Daily send cap and send log (TC-09, TC-03).
- **Requirements:** FR-13, FR-32, FR-33, FR-34, FR-47, NFR-07, TC-03, TC-09.
- **Tests:** Hebrew text is counted as 70 characters per segment. The recipient count matches the directory. A failed send is retried and logged. A high-urgency request triggers an alert to the maintenance manager.
- **Done when:** A high-urgency request sends an alert, and a failed send is retried and logged.

### Step 7: Guest parking
- **Scope:** Day view of slots (available, reserved, taken). One-tap reservation with guest name, vehicle number, host, and time range. Cancellation until arrival time. Database constraint that prevents two reservations for the same slot and time. The gate integration is mocked until the vendor interface is confirmed (FR-15, FR-22 to FR-25, TC-08, TC-20).
- **Requirements:** FR-15, FR-22 to FR-25, TC-08, TC-20.
- **Tests:** Two simultaneous reservations for one slot produce one success and one clear error. Cancellation after arrival time is refused. Guest data is visible only to the host and managers.
- **Done when:** Two simultaneous reservations for one slot produce one success and one error.

### Step 8: Events and space booking
- **Scope:** Event form (FR-26). Room availability checked against the calendar and capacity (FR-27). Equipment selection with exact quantities (FR-28). Versioned quantity lines. Approval flow by the building manager. Changes after approval require the maintenance manager (FR-29, FR-30). "My events" (FR-31). Stock limits are shown only when the data source is confirmed (TC-19).
- **Requirements:** FR-26 to FR-31, TC-08, TC-19.
- **Tests:** Only available rooms are offered for the chosen time and capacity. An approved quantity change creates an update for operations. A change after approval without the maintenance manager is refused.
- **Done when:** An approved quantity change creates a visible update for the operations team.

### Step 9: Preventive maintenance
- **Scope:** Maintenance plans with system, frequency (weekly, monthly, quarterly, annual), owner or vendor, last done date, and next due date (FR-35, FR-40). Task generator as a scheduled job with a unique key per schedule and date (FR-36, TC-11). Assignment (FR-37). Reminders before the due date and an alert for overdue tasks (FR-38). Completion board with percentage and calendar (FR-39). Compliance report (FR-41).
- **Requirements:** FR-35 to FR-41, TC-11.
- **Tests:** Running the generator twice creates each task once. A missed run is caught up on the next run. Overdue tasks trigger an alert. The completion percentage is correct for known test data.
- **Done when:** Running the generator twice creates each task exactly once.

### Step 10: Compliance certificates
- **Scope:** Certificate records with system, inspection type, inspecting body, dates, and a scanned file (FR-42, FR-43). Private file storage with access through short-lived links (FR-48, TC-05). Reminder lead time per certificate (FR-44). Escalating reminders that stop when a renewal is uploaded (FR-45, TC-12). Expired certificates are shown in red at the top of the dashboard (FR-46). Reminders go to the maintenance manager and an optional contact (FR-47).
- **Requirements:** FR-42 to FR-48, TC-05, TC-12.
- **Tests:** Counts for valid, expiring within 30 days, and expired are correct. Uploading a renewal cancels pending reminders. Reminder frequency increases near expiry. Files are not reachable without an access check.
- **Done when:** A renewed certificate cancels its pending reminders.

### Step 11: Dashboard and reports
- **Scope:** Daily summary job that precomputes figures (TC-13). Dashboard with open requests, opened this month, average handling time, SLA compliance, recent requests, requests by category, six-month trend, monthly cost by category, response time per technician or vendor, guest parking utilization, overdue plans, and total cost (FR-52 to FR-57). Start only after the SLA and cost definitions are confirmed (TC-22). Every figure shows its source and date.
- **Requirements:** FR-52 to FR-57, NFR-10, TC-13, TC-22.
- **Tests:** Each dashboard figure matches a hand-calculated result on the test data. The SLA rule counts working hours only, Sunday to Thursday (TC-10). Figures show the date of the last refresh.
- **Done when:** The dashboard figures match the test data exactly.

### Step 12: Launch hardening
- **Scope:** Accessibility checks against WCAG 2.1 AA for Hebrew content (TC-21). Performance on a throttled mobile connection (TC-23). Monitoring and error reporting. Backups with a tested restore. Retention jobs (NFR-12, NFR-05). Final review of the privacy notice with legal.
- **Requirements:** NFR-05, NFR-07, NFR-08, NFR-11, NFR-12, TC-21, TC-23.
- **Tests:** Accessibility scan has no critical issues. Pages load within the agreed target on a throttled connection. A restore from backup succeeds on a test copy. Retention jobs remove records older than the configured period.
- **Done when:** A pilot group of employees has used the app for one week without critical issues, and the legal review is complete.

---

## 8. Final acceptance

After step 12, produce `docs/validation/final.md` with:

- A table of every requirement ID (FR, NFR, TC), with the step that built it, the test names that cover it, and its status (passed, open, or deferred).
- Any open items, with the owner named in the requirements document.
- The pilot plan: group, duration, and the feedback form.

Then ask the user to confirm the pilot start.
