# Real-Time Logistics Monitoring for Myanmar Trading

- **Course:** AIE-F B2 — Assignment 5
- **Prototype Deadline:** 18 September 2026
- **Live Demo:** 20 September 2026
- **Version:** 1.0

---

## 1. Product Overview

**This** is a web-based logistics monitoring system designed for transportation and trading activities in Myanmar.

The system allows:

- **Traders** to create and monitor shipments.
- **Drivers** to update shipment status and location.
- **Administrators** to monitor all shipments, manage route conditions, and broadcast alerts.

The system focuses on problems that can occur during transportation in Myanmar, including:

- Difficulties knowing the current location of a vehicle.
- Delays during transportation.
- Route or border-gate closures.
- Poor communication between traders and drivers.
- Internet connectivity problems.
- Difficulty monitoring multiple shipments at the same time.

The prototype will use **simulated GPS locations** rather than real vehicle GPS hardware.

---

## 2. Product Vision

> **To provide a simple, real-time logistics monitoring system that helps Myanmar traders, drivers, and administrators understand where shipments are, what is happening to them, and whether route problems may cause delays.**

---

## 3. Problem Statement

During transportation, traders may not always have an easy way to know:

- Where their shipment currently is.
- Whether the driver has reached an important location.
- Whether a shipment is delayed.
- Whether a major route has been closed.
- Whether a route problem affects their shipment.
- Whether a driver has successfully reported an update.

Drivers may also face:

- Poor internet connectivity.
- Difficulty communicating updates.
- Delays at checkpoints.
- Route disruptions.

Administrators need a centralized view of:

- Active shipments.
- Shipment locations.
- Route conditions.
- Delays.
- Important alerts.

---

## 4. Proposed Solution

This provides three role-based interfaces:

### Admin

Monitors and manages the entire logistics system.

### Trader

Creates shipments and monitors their own shipments.

### Driver

Updates shipment progress, location, and documents.

The system also provides:

- Shipment timeline
- Simulated GPS tracking
- Myanmar map
- Route status
- Route closure alerts
- Real-time updates
- Offline update simulation
- Document/photo upload

---

## 5. Target Users

### 5.1 Admin

The person responsible for monitoring and managing logistics activities.

### 5.2 Trader

A person or business sending goods from one location to another.

### 5.3 Driver

The person transporting the shipment.

---

## 6. User Roles and Permissions

| Feature | Admin | Trader | Driver |
| ----- | ----- | ----- | ----- |
| View all shipments | Yes | No | No |
| View own shipments | Yes | Yes | Assigned only |
| Create shipment | Yes | Yes | No |
| Update shipment status | Yes | No | Yes |
| Update location | Yes | No | Yes |
| View map | Yes | Yes | Yes |
| Manage routes | Yes | No | No |
| Close/open route | Yes | No | No |
| Receive alerts | Yes | Yes | Yes |
| Upload documents | Yes | No | Yes |
| Offline updates | No | No | Yes |

---

## 7. Authentication

Users must log in before accessing the system.

After login, the system identifies the user's role and redirects them to the appropriate dashboard.

Example:

```text
Login
↓
Check user role
↓
Admin   → Admin Dashboard
Trader  → Trader Dashboard
Driver  → Driver Dashboard
```

---

## 8. Role-Based Access Control

The system must enforce permissions based on user roles.

Users must not be able to access functions that belong to another role simply by manually entering a URL.

For example:

- A Trader must not access the Admin route-management page.
- A Driver must not close a route.
- A Trader must not modify another trader's shipment.
- An Admin can view all shipments.

---

## 9. Admin Dashboard

The Admin Dashboard provides an overview of the entire logistics system.

### Dashboard information

The Admin should be able to see:

- Total shipments
- Active shipments
- Delayed shipments
- Delivered shipments
- Closed routes
- Recent alerts
- Current vehicle locations

### Main sections

#### Shipment Overview

Displays shipment status and information.

#### Live Map

Displays simulated truck locations.

#### Route Management

Allows Admin to open or close routes.

#### Alerts

Displays important system alerts.

---

## 10. Trader Dashboard

The Trader Dashboard allows traders to manage and monitor their own shipments.

The Trader can:

- Create a shipment.
- View shipment list.
- View shipment details.
- View shipment timeline.
- View truck location.
- Receive route alerts.
- Receive delay alerts.

---

## 11. Driver Dashboard

The Driver Dashboard is designed to be simple because drivers may use mobile phones and may have unreliable internet connectivity.

The Driver can:

- View assigned shipment.
- View destination.
- Update shipment status.
- Update simulated location.
- Report checkpoint arrival.
- Upload document/photo.
- Work in simulated offline mode.
- Synchronize pending updates when connection returns.

---

## 12. Shipment

A shipment represents goods being transported from an origin to a destination.

Each shipment should contain:

- Tracking number
- Trader
- Driver
- Origin
- Destination
- Route
- Cargo description
- Current status
- Current latitude
- Current longitude
- Created date
- Updated date

Example:

- **Tracking Number:** MYT-2026-001
- **Cargo:** Agricultural products
- **Origin:** Yangon
- **Destination:** Muse
- **Driver:** Aung Aung
- **Route:** Yangon → Mandalay → Lashio → Muse
- **Status:** In Transit

---

## 13. Shipment Statuses

The system should use simple shipment stages.

### 13.1 Requested

The trader has created a shipment request.

**Meaning:** ကုန်ပစ္စည်း ပို့ဆောင်ရန် တောင်းဆိုထားသည်။

---

### 13.2 Picked Up

The driver has collected the goods.

**Meaning:** ကားသမားက ကုန်ပစ္စည်းကို လက်ခံယူပြီးဖြစ်သည်။

---

### 13.3 In Transit

The shipment is currently being transported.

**Meaning:** ကုန်ပစ္စည်းသည် လမ်းပေါ်တွင် ပို့ဆောင်နေသည်။

---

### 13.4 Checkpoint

The driver has reached a designated checkpoint.

**Meaning:** ကားသည် စစ်ဆေးရေးနေရာသို့ ရောက်ရှိနေသည်။

---

### 13.5 Delayed

The shipment is experiencing a delay.

**Meaning:** ပို့ဆောင်မှုတွင် နောက်ကျမှု ဖြစ်နေသည်။

---

### 13.6 Customs — Conditional

**Customs should NOT be required for every shipment.**

This stage is used only when the shipment involves an international border/trade process.

For example, a shipment traveling toward a border crossing may enter a customs-related stage when appropriate.

**Meaning:** အကောက်ခွန်နှင့် သက်ဆိုင်သော စစ်ဆေးမှုများ ပြုလုပ်နေသည်။

For a purely domestic shipment, this stage is skipped.

---

### 13.7 Delivered

The shipment has reached its destination.

**Meaning:** ကုန်ပစ္စည်းကို သတ်မှတ်ထားသော နေရာသို့ ပို့ဆောင်ပြီးဖြစ်သည်။

---

## 14. Shipment Flow

For a normal domestic shipment:

```text
Requested
↓
Picked Up
↓
In Transit
↓
Checkpoint
↓
In Transit
↓
Delivered
```

If a problem occurs:

```text
In Transit
↓
Delayed
↓
In Transit
```

For a shipment involving an international border:

```text
Requested
↓
Picked Up
↓
In Transit
↓
Checkpoint
↓
Customs
↓
In Transit
↓
Delivered
```

Therefore, **Customs is an optional stage, not a mandatory stage.**

---

## 15. Shipment Timeline

Each shipment should display a visual timeline.

Example:

```text
- ✓ Shipment Requested
↓
- ✓ Goods Picked Up
↓
- ✓ In Transit
↓
- ✓ Checkpoint Reached
↓
● In Transit
↓
○ Delivered
```

The timeline should show:

- Status
- Time
- Location
- Optional description

---

## 16. GPS Tracking

The prototype will simulate vehicle location.

A real GPS device is NOT required.

The Driver can select predefined locations.

Example route:

```text
Yangon
↓
Mandalay
↓
Lashio
↓
Muse
```

The Driver can press:

**Update Location**

The system updates:

- Latitude
- Longitude
- Current location

The Admin and Trader can see the updated position.

---

## 17. Myanmar Map

The system will display a Myanmar map using:

- Leaflet
- OpenStreetMap

The map will show:

- Shipment location
- Truck marker
- Route information

The project does not need to create its own Myanmar map.

---

## 18. Simulated GPS

Because this is a prototype, GPS movement will be simulated.

Example:

- Location 1 → Yangon
- Location 2 → Mandalay
- Location 3 → Lashio
- Location 4 → Muse

When the Driver clicks **Update Location**, the truck marker moves to the next predefined location.

This demonstrates the concept of real-time tracking without requiring physical GPS hardware.

---

## 19. Real-Time Updates

The system should use real-time communication so that users do not need to refresh the page manually.

Example:

```text
Driver
↓
Updates location
↓
Database
↓
Real-time update
↓
Admin Dashboard
Trader Dashboard
```

The same approach is used for alerts.

---

## 20. Route Management

Admins can manage important transportation routes.

Each route has:

- Route name
- Starting location
- Destination
- Current status
- Description
- Last updated time

Possible route statuses:

- `OPEN`
- `CLOSED`

---

## 21. Myanmar-Specific Routes

The prototype will demonstrate important Myanmar transportation routes.

Example:

### Route 1

Yangon → Mandalay → Lashio → Muse

### Route 2

Yangon → Bago → Naypyidaw → Myawaddy

These are used primarily for demonstration purposes.

The system should not claim that these routes represent all real-world logistics routes or current operating conditions.

---

## 22. Route Closure

An Admin can change a route from:

OPEN

to:

CLOSED

Example:

> Muse Route → CLOSED

The system then identifies active shipments associated with that route.

---

## 23. Automatic Alerts

When a route is closed, affected users receive an alert.

Example:

> **Muse လမ်းကြောင်း ပိတ်ထားပါသည်။ သင်၏ကုန်ပစ္စည်း ပို့ဆောင်မှု နောက်ကျနိုင်ပါသည်။**

The alert may be sent to:

- Trader
- Driver
- Admin

---

## 24. Alert Severity

Alerts can have different levels.

### Normal

General information.

### Warning

Possible delay or route problem.

### High

Important disruption requiring attention.

Example:

```text
HIGH
Muse လမ်းကြောင်း ပိတ်ထားပါသည်။
သင်၏ပို့ဆောင်မှု နောက်ကျနိုင်ပါသည်။
```

---

## 25. Offline Capability

The Driver may lose internet connectivity during transportation.

The prototype will simulate this situation.

When the Driver is offline:

```text
Internet unavailable
↓
Driver updates status
↓
Update stored locally
↓
Pending update created
```

When the connection returns:

```text
Internet restored
↓
Pending updates synchronized
↓
Database updated
```

---

## 26. Offline User Interface

The Driver should see a clear indicator.

Example:

```text
🔴 Offline
Pending updates: 2
```

After reconnection:

```text
🟢 Online
2 updates synchronized
```

---

## 27. Document Upload

Drivers can upload photos related to a shipment.

Example:

- Delivery document
- Cargo document
- Checkpoint document
- Other relevant photo

The prototype will use cloud storage.

The system stores:

- File name
- File location
- Shipment
- Driver
- Document type
- Upload time

---

## 28. Database

The prototype will use Supabase PostgreSQL.

Main tables:

- `profiles`
- `routes`
- `shipments`
- `shipment_events`
- `alerts`
- `documents`

---

## 29. Profiles Table

Stores user information.

Fields:

- `id`
- `name`
- `email`
- `role`
- `created_at`

Possible roles:

- `ADMIN`
- `TRADER`
- `DRIVER`

---

## 30. Routes Table

Stores transportation routes.

Fields:

- `id`
- `name`
- `origin`
- `destination`
- `status`
- `description`
- `updated_at`

---

## 31. Shipments Table

Stores shipment information.

Fields:

- `id`
- `tracking_number`
- `trader_id`
- `driver_id`
- `route_id`
- `cargo_description`
- `origin`
- `destination`
- `status`
- `latitude`
- `longitude`
- `created_at`
- `updated_at`

---

## 32. Shipment Events Table

Stores shipment history.

Fields:

- `id`
- `shipment_id`
- `status`
- `description`
- `latitude`
- `longitude`
- `created_by`
- `created_at`

This table allows the system to build the shipment timeline.

---

## 33. Alerts Table

Stores notifications.

Fields:

- `id`
- `route_id`
- `shipment_id`
- `recipient_id`
- `message`
- `severity`
- `is_read`
- `created_at`

---

## 34. Documents Table

Stores uploaded document information.

Fields:

- `id`
- `shipment_id`
- `driver_id`
- `file_name`
- `file_url`
- `document_type`
- `created_at`

---

## 35. Security Requirements

The system must protect user access.

Requirements:

- Authentication required.
- Role-based permissions.
- Users can only access authorized data.
- Traders can only manage their own shipments.
- Drivers can only update assigned shipments.
- Only Admins can manage route status.
- Only authorized users can upload documents.

---

## 36. Realtime Architecture

The system will use Supabase Realtime.

Important real-time events:

### GPS update

```text
Driver changes location
↓
Database updated
↓
Admin/Trader map updates
```

### Route closure

```text
Admin closes route
↓
Affected shipments identified
↓
Alerts created
↓
Trader/Driver receives alert
```

---

## 37. Main Application Pages

### Public

- `/login`

### Admin

- `/admin`
- `/admin/shipments`
- `/admin/routes`
- `/admin/alerts`

### Trader

- `/trader`
- `/trader/shipments`
- `/trader/shipments/[id]`
- `/trader/request`

### Driver

- `/driver`
- `/driver/shipment`
- `/driver/documents`

---

## 38. Main UI Components

Reusable components should include:

- `Navbar`
- `Sidebar`
- `ShipmentCard`
- `ShipmentTimeline`
- `TrackingMap`
- `RouteStatus`
- `AlertCard`
- `OfflineIndicator`
- `StatusBadge`

---

## 39. User Experience Requirements

The system should be:

- Simple
- Easy to understand
- Mobile-friendly
- Fast
- Clear
- Suitable for users with limited technical knowledge

The Driver interface should be especially simple.

Important actions should be large and easy to identify.

---

## 40. Main Trader Journey

```text
Login
↓
Trader Dashboard
↓
Create Shipment
↓
Shipment Created
↓
View Shipment
↓
View Timeline
↓
View Truck Location
↓
Receive Route Alert
↓
Monitor Shipment
↓
Delivered
```

---

## 41. Main Driver Journey

```text
Login
↓
Driver Dashboard
↓
View Assigned Shipment
↓
Pick Up Goods
↓
Start Transportation
↓
Update Location
↓
Reach Checkpoint
↓
Update Status
↓
Upload Document
↓
Continue Transportation
↓
Delivered
```

---

## 42. Main Admin Journey

```text
Login
↓
Admin Dashboard
↓
View All Shipments
↓
View Map
↓
Monitor Routes
↓
Close Muse Route
↓
System Identifies Affected Shipments
↓
Alerts Generated
↓
Trader/Driver Receives Alert
```

---

## 43. Critical Live Demo Scenario

The main demonstration will use one shipment.

### Shipment

- **Tracking Number:** MYT-2026-001
- **Cargo:** Agricultural products
- **Origin:** Yangon
- **Destination:** Muse
- **Driver:** Aung Aung

---

### Step 1 — Trader creates shipment

Trader creates:

Yangon → Muse

Shipment status:

Requested

---

### Step 2 — Driver receives shipment

Driver accepts/starts the shipment.

Status:

Picked Up

---

### Step 3 — Driver starts transportation

Status:

In Transit

---

### Step 4 — Driver updates GPS

Driver moves the simulated truck:

```text
Yangon
↓
Mandalay
↓
Lashio
```

Trader sees the truck moving on the map.

---

### Step 5 — Admin closes route

Admin changes:

Muse Route

OPEN → CLOSED

---

### Step 6 — System generates alert

The affected shipment receives:

> Muse လမ်းကြောင်း ပိတ်ထားပါသည်။ သင်၏ကုန်ပစ္စည်း ပို့ဆောင်မှု နောက်ကျနိုင်ပါသည်။

---

### Step 7 — Driver goes offline

Driver switches the prototype into offline mode.

Driver updates:

Checkpoint ရောက်ရှိ

The update is stored locally.

---

### Step 8 — Driver reconnects

Driver switches back online.

The pending update synchronizes with the database.

---

### Step 9 — Shipment continues

Status returns to:

In Transit

---

### Step 10 — Delivery

Driver reaches the destination.

Status:

Delivered

---

## 44. AI / Vibe Coding Requirements

The project will use AI-assisted development tools such as:

- ChatGPT
- Claude
- Cursor
- GitHub Copilot

AI will be used for:

- UI generation
- Component creation
- Database queries
- API logic
- Debugging
- Documentation
- Testing assistance

---

## 45. AI Engineering Process

For each major AI-generated feature, the team should:

1. Define the requirement.
2. Write a clear prompt.
3. Generate the implementation.
4. Review the generated code.
5. Test the feature.
6. Identify hallucinations or incorrect assumptions.
7. Correct the implementation.
8. Document the final result.

---

## 46. Hallucination Management

The team must not blindly trust AI-generated code.

Potential problems include:

- Incorrect Supabase APIs.
- Incorrect database relationships.
- Incorrect authentication logic.
- Fake or outdated library methods.
- Incorrect assumptions about logistics workflows.

The team should verify generated code against:

- Official documentation
- Actual application behavior
- Database schema
- Test results

---

## 47. Technical Stack

### Frontend

- Next.js
- TypeScript
- Tailwind CSS
- Lucide React

### Backend / BaaS

- Supabase

Including:

- Supabase Auth
- Supabase PostgreSQL
- Supabase Realtime
- Supabase Storage

### Map

- Leaflet
- OpenStreetMap

### Offline

- localStorage / IndexedDB

### Deployment

- Vercel

### Version Control

- GitHub

---

## 48. Project Structure

```text
This/
├── app/
│   ├── login/
│   ├── admin/
│   ├── trader/
│   └── driver/
│
├── components/
│   ├── ui/
│   ├── layout/
│   ├── shipment/
│   ├── map/
│   ├── alerts/
│   └── driver/
│
├── lib/
│   ├── supabase/
│   ├── services/
│   └── offline/
│
├── types/
│
├── public/
│
├── docs/
│   ├── architecture.md
│   ├── database-schema.md
│   ├── demo-scenario.md
│   └── ai-engineering-log.md
│
├── .env.local
├── .gitignore
├── package.json
└── README.md
```

---

## 49. Non-Goals

The prototype will NOT attempt to build:

- Real GPS hardware integration.
- A real driver mobile application.
- Real-time satellite tracking.
- Full customs management.
- Full import/export documentation management.
- Payment processing.
- Fleet management.
- Complex route optimization.
- AI-based ETA prediction.
- Microservices architecture.
- Kubernetes infrastructure.

These may be future improvements but are outside the MVP.

---

## 50. Important Scope Decision: Customs

Customs is **not a core requirement for every shipment**.

The product supports both:

### Domestic transportation

Example:

Yangon → Mandalay

No Customs stage is required.

### Border-related transportation

Example:

Yangon → Lashio → Muse

If the shipment is actually crossing an international border, a Customs stage may be used.

Therefore:

> **Customs is a conditional shipment stage rather than a mandatory stage.**

This keeps the product realistic without making the prototype unnecessarily complicated.

---

## 51. MVP — Must Have

The following features are required for the live prototype:

- Login
- Role-based access
- Admin dashboard
- Trader dashboard
- Driver dashboard
- Shipment creation
- Shipment status
- Shipment timeline
- Myanmar map
- Simulated GPS
- Real-time updates
- Route management
- Muse route
- Route open/close
- Automatic alerts
- Offline update simulation

---

## 52. Should Have

If development time allows:

- Document upload
- Shipment filtering
- Alert history
- Mobile-friendly UI
- Multiple routes
- Better shipment search

---

## 53. Nice to Have

Only implement these if the MVP is already stable:

- Analytics
- Charts
- Route history
- Delivery statistics
- ETA estimation
- Multiple drivers
- Advanced search
- Real GPS integration

---

## 54. Success Criteria

The prototype will be considered successful if the team can demonstrate:

### Role Management

- ✓ Three different roles work correctly.

### Shipment Management

- ✓ Trader can create a shipment.

### Tracking

- ✓ Driver can update shipment location.

### Map

- ✓ Truck location appears on Myanmar map.

### Realtime

- ✓ Location changes appear without manual refresh.

### Route Management

- ✓ Admin can close a route.

### Alert

- ✓ Affected users receive the route closure alert.

### Offline

- ✓ Driver can make an update while offline.

### Synchronization

- ✓ Offline update synchronizes after reconnection.

### Delivery

- ✓ Shipment can eventually reach Delivered status.

---

## 55. Development Roadmap

### Phase 1 — Planning

- ✓ Product Requirements Document
- ✓ Architecture
- ✓ Database design
- ✓ Demo scenario

### Phase 2 — Setup

- Create Next.js project
- Configure Tailwind
- Create Supabase project
- Configure environment variables

### Phase 3 — Authentication

- Login
- User roles
- Role-based routing
- Permission checks

### Phase 4 — Database

- Create tables
- Relationships
- Security policies
- Seed demo data

### Phase 5 — Dashboards

- Admin Dashboard
- Trader Dashboard
- Driver Dashboard

### Phase 6 — Shipment

- Create shipment
- View shipment
- Status updates
- Timeline

### Phase 7 — Map

- Install Leaflet
- Display Myanmar map
- Display truck marker
- Simulate GPS movement

### Phase 8 — Realtime

- Realtime shipment updates
- Realtime GPS
- Realtime alerts

### Phase 9 — Route Alerts

- Route management
- Open/close route
- Detect affected shipments
- Generate alerts

### Phase 10 — Offline

- Offline indicator
- Local update queue
- Synchronization

### Phase 11 — Documents

- Upload photo
- Store document information

### Phase 12 — Testing

- Test each role
- Test permissions
- Test shipment flow
- Test GPS
- Test alerts
- Test offline synchronization

### Phase 13 — Deployment

- Deploy to Vercel
- Test production version
- Prepare demo accounts

### Phase 14 — Presentation

- 5-minute problem/solution
- 15-minute live demo
- 10-minute AI engineering reflection

---

## 56. Final Product Flow

### 1. Login

User opens the system and logs in.

The system identifies the user's role:

- Admin → Admin Dashboard
- Trader → Trader Dashboard
- Driver → Driver Dashboard

---

### 2. Trader Flow

Trader logs in.

→ Opens Trader Dashboard

→ Clicks **Create Shipment**

→ Enters:

- Cargo description
- Origin
- Destination
- Route
- Driver

→ Clicks **Create Shipment**

→ System creates a shipment with status:

**REQUESTED — တောင်းဆိုထားသည်**

→ Trader can view:

- Tracking number
- Shipment status
- Shipment timeline
- Driver location
- Route status
- Alerts

---

### 3. Driver Flow

Driver logs in.

→ Opens Driver Dashboard

→ Views assigned shipment

→ Clicks **Accept / Start Shipment**

→ Updates status:

**PICKED_UP — ကုန်ပစ္စည်း လက်ခံပြီး**

→ Driver starts transportation

→ Updates status:

**IN_TRANSIT — လမ်းပေါ်တွင် ပို့ဆောင်နေသည်**

→ Driver updates simulated GPS location

Example:

Yangon → Mandalay → Lashio → Muse

→ Admin and Trader see the updated truck location in real time.

---

### 4. Checkpoint Flow

Driver reaches a checkpoint.

→ Clicks **Arrived at Checkpoint**

→ Status becomes:

**CHECKPOINT — စစ်ဆေးရေးဂိတ် ရောက်ရှိ**

→ Driver can upload a checkpoint document/photo.

→ Shipment timeline is updated.

→ Driver continues transportation.

→ Status returns to:

**IN_TRANSIT — လမ်းပေါ်တွင် ပို့ဆောင်နေသည်**

---

### 5. Customs Flow — Border Shipment Only

If the shipment is a border-related shipment:

→ Driver reaches the border/customs area

→ Status becomes:

**CUSTOMS — အကောက်ခွန် စစ်ဆေးနေသည်**

→ Customs/document process is simulated.

→ After completion:

**IN_TRANSIT — လမ်းပေါ်တွင် ပို့ဆောင်နေသည်**

For a normal domestic shipment, the Customs step is skipped.

---

### 6. Admin Route Management Flow

Admin logs in.

→ Opens **Route Management**

→ Views active routes.

Example:

- Yangon → Mandalay → Lashio → Muse
- Yangon → Bago → Naypyidaw → Myawaddy

→ Admin can change a route:

**OPEN → CLOSED**

Example:

**Muse Route: CLOSED**

→ System identifies active shipments using that route.

→ System creates an alert.

→ Trader receives:

**"Muse လမ်းကြောင်း ပိတ်ထားပါသည်။ သင်၏ကုန်ပစ္စည်း ပို့ဆောင်မှု နောက်ကျနိုင်ပါသည်။"**

→ Driver also receives the alert.

→ Shipment can be marked:

**DELAYED — နောက်ကျနေသည်**

---

### 7. Driver Offline Flow

Driver loses internet connection.

→ Driver switches to simulated **Offline Mode**

→ Driver updates shipment status/location.

Example:

**CHECKPOINT — စစ်ဆေးရေးဂိတ် ရောက်ရှိ**

→ System cannot immediately send the update to Supabase.

→ Update is saved locally.

→ UI shows:

**Offline — Pending Updates: 1**

→ Internet connection returns.

→ Driver clicks **Sync Updates**

→ Pending updates are uploaded to Supabase.

→ UI shows:

**Online — Updates Synchronized**

→ Admin and Trader receive the updated shipment information.

---

### 8. Real-Time Tracking Flow

Driver updates location.

→ Location is saved to the database.

→ Supabase Realtime sends the update.

→ Admin Dashboard updates automatically.

→ Trader Dashboard updates automatically.

→ Truck marker moves on the map without refreshing the page.

---

### 9. Delivery Flow

Driver reaches the destination.

→ Driver clicks **Mark as Delivered**

→ Status becomes:

**DELIVERED — ပို့ဆောင်ပြီး**

→ Shipment timeline is completed.

→ Trader receives the final delivery status.

→ Admin can see the completed shipment.

---

### Complete Shipment Flow

#### Domestic Shipment

```text
REQUESTED
↓
PICKED_UP
↓
IN_TRANSIT
↓
CHECKPOINT
↓
IN_TRANSIT
↓
DELIVERED
```

#### Border Shipment

```text
REQUESTED
↓
PICKED_UP
↓
IN_TRANSIT
↓
CHECKPOINT
↓
CUSTOMS
↓
IN_TRANSIT
↓
DELIVERED
```

#### If Route Is Closed

```text
IN_TRANSIT
↓
ROUTE CLOSED
↓
ALERT SENT
↓
DELAYED
↓
ROUTE REOPENED
↓
IN_TRANSIT
↓
DELIVERED
```

---

### Final Demo Flow

1. Trader logs in.
2. Trader creates a shipment from Yangon to Muse.
3. Shipment status becomes **REQUESTED**.
4. Driver logs in and sees the assigned shipment.
5. Driver marks it **PICKED_UP**.
6. Driver marks it **IN_TRANSIT**.
7. Driver updates simulated GPS location.
8. Admin sees the truck moving on the map.
9. Driver reaches a checkpoint and marks **CHECKPOINT**.
10. Admin closes the Muse route.
11. System automatically sends an alert to the affected Trader and Driver.
12. Shipment becomes **DELAYED**.
13. Driver switches to **Offline Mode**.
14. Driver makes a status/location update.
15. The update is saved locally as a pending update.
16. Driver reconnects to the internet.
17. Pending update synchronizes automatically.
18. Admin reopens the Muse route.
19. Shipment continues **IN_TRANSIT**.
20. Driver reaches Muse.
21. Driver marks the shipment **DELIVERED**.
22. Trader sees the completed shipment timeline.

---

## 57. Product Owner Decision

The core product principle is:

> **Keep the system simple enough to demonstrate reliably, but realistic enough to represent an actual logistics monitoring workflow in Myanmar.**

The prototype does not attempt to solve the entire logistics industry.

It focuses on one important problem:

> **“Where is my shipment, what is happening to it, and will a route problem affect it?”**

The product therefore prioritizes:

**Shipment Tracking → GPS → Route Status → Alerts → Offline Updates**

over complicated logistics functions.

---

## 58. Final Product Definition

**This is a role-based, real-time logistics monitoring web application for Myanmar transportation and trading.**

It connects:

**Trader + Driver + Admin**

through:

**Shipment Tracking + Simulated GPS + Route Monitoring + Real-Time Alerts + Offline Synchronization.**

The prototype supports normal domestic transportation and can also represent border-related shipments. Customs is included only as a **conditional stage** when relevant, rather than forcing every shipment through Customs.
