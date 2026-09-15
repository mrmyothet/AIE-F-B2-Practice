## What you need to deliver

According to assignment-5/README.md, you need a deployed Myanmar logistics tracking prototype and a 30-minute group presentation.

The assignment folder currently contains only the instructions, so implementation still needs to start.

- Project deadline: 18 September 2026.
- Presentation: 20 September 2026. The brief labels this “SAT,” but that date is Sunday—confirm the intended day with your instructor.

## Steps to finish

### 1. Define one complete demo scenario

Build around this shipment lifecycle:

> Trader requests transport → Admin assigns a driver → Driver updates location and shipment status → Admin closes the shipment’s border gate → Trader receives an alert → Driver completes delivery.

Use sample shipments through Muse and Myawaddy. Prioritize making this complete flow work before adding extra features.

### 2. Choose the stack and divide responsibilities

The brief suggests React/Next.js, Tailwind, and Firebase/Supabase. Choose one frontend and one backend option your group can work with.

Divide the work into:

- Frontend: dashboards, tracking map, driver mobile layout.
- Backend: authentication, permissions, data, live updates.
- Integration and presentation: testing, deployment, demo data, AI development notes.

### 3. Design the data model

Start with these entities:

Entity Main information
━━━━━━━━━━━━━━━━━━ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Users Name, role
────────────────── ────────────────────────────────────────────────────────────────────────────
Shipments Trader, assigned driver, cargo, origin, destination, route, current status
────────────────── ────────────────────────────────────────────────────────────────────────────
Shipment events Shipment, status, timestamp, notes, location
────────────────── ────────────────────────────────────────────────────────────────────────────
Routes/gates Name, open/delayed/closed status, update message
────────────────── ────────────────────────────────────────────────────────────────────────────
Location updates Shipment, coordinates, timestamp
────────────────── ────────────────────────────────────────────────────────────────────────────
Documents Shipment, uploaded photo reference, uploader
────────────────── ────────────────────────────────────────────────────────────────────────────
Alerts Recipient, shipment or route, message, read status

Store document photos in file storage and their references in the database.

### 4. Implement login and role permissions

Create three demo accounts and enforce access in the backend:

- Admin: sees all shipments, assigns drivers, changes gate statuses, broadcasts alerts.
- Trader: creates transport requests and sees only their shipments and alerts.
- Driver: sees assigned shipments and submits location, status, and document updates.

Hiding buttons alone does not enforce permissions.

### 5. Build the shipment workflow

Create the essential screens:

- Trader: request form, shipment list, shipment tracking page.
- Admin: all shipments, driver assignment, gate controls, alert form.
- Driver: mobile-friendly assigned shipment page with update buttons and photo upload.

Display a timeline such as:

Requested → Picked Up → In Transit → Customs → Delivered

Keep timestamped events so the timeline shows shipment history.

### 6. Add simulated live tracking

- Display a truck marker on a map.
- Move it through predefined coordinates using a simulation control or timer.
- Save location updates and refresh the trader’s tracking view automatically.
- Show the latest update time and label the GPS data as simulated.

### 7. Implement gate closures and alerts

When an admin changes a gate to Closed or Delayed:

1. Save the gate status and explanation.
2. Find active shipments using that route.
3. Create alerts for their traders.
4. Update affected tracking screens automatically.

Also support a manual admin broadcast and a driver-reported delay.

### 8. Demonstrate offline behavior

The brief allows a proposal or simulation. A demonstrable simulation would:

- Provide an Offline mode toggle in the driver view.
- Queue location and status updates locally.
- Display the number of pending updates.
- Sync them when connectivity returns.
- Prevent duplicate events if synchronization retries.

Explain separately how photo uploads would behave offline.

### 9. Test and deploy

Verify the complete scenario using separate browser sessions for each role:

- Traders cannot access another trader’s shipments.
- Drivers can update only assigned shipments.
- Location and status changes reach the tracking dashboard.
- Gate changes alert the correct traders.
- Document photos upload and display.
- Offline updates survive a refresh and sync once.
- The deployed application supports the same flow.

Prepare demo accounts, sample data, and a repeatable way to reset the demo.

### 10. Prepare the presentation and AI evidence

Follow the required timing:

Section Time Content
━━━━━━━━━━━━━━━━━━━━━━━━━━━ ━━━━━━━━━━━━ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Problem and solution 5 minutes Myanmar logistics challenges and your approach
─────────────────────────── ──────────── ───────────────────────────────────────────────────────────────────────
Live demo 15 minutes All three roles, shipment lifecycle, gate closure, offline simulation
─────────────────────────── ──────────── ───────────────────────────────────────────────────────────────────────
AI engineering reflection 10 minutes Tools, effective prompts, failures, fixes

Record AI prompts and corrections during development. Keep concrete examples of generated code you changed, why it failed, and how you verified the fix.

## Suggested schedule

- 15 September: agree on scope, design data, scaffold the app, implement authentication.
- 16 September: complete role screens and shipment workflow.
- 17 September: add tracking, alerts, uploads, and offline simulation; deploy.
- 18 September: fix integration issues, verify requirements, submit.
- 19 September: rehearse the presentation and prepare a backup demo recording.
