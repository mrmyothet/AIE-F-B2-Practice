# Feature roadmap

Status: planning complete; implementation has not started. Source documents: [assignment](../README.md) and [PRD](../PRD.md).

Each change contains proposal.md (scope), design.md (technical approach), specs/<capability>/spec.md (testable behavior), and tasks.md (implementation checkboxes with verification). Build and verify one change before starting its dependents. The order below is a recommended sequence; prerequisites are documented in each proposal.

## Build order

| Order | Change | Demo checkpoint | Depends on |
| --- | --- | --- | --- |
| 1 | [Login and role access](changes/add-role-access/proposal.md) | Three roles log in; wrong-role access fails. | — |
| 2 | [Create and view assigned shipments](changes/add-shipment-requests/proposal.md) | Trader creates a request; only owner, assigned Driver and Admin see it. | 1 |
| 3 | [Status updates and timeline](changes/add-shipment-progress/proposal.md) | Driver completes the lifecycle; history and counts update. | 2 |
| 4 | [Simulated GPS and map](changes/add-live-tracking/proposal.md) | Driver moves the marker; authorized maps update live. | 3 |
| 5 | [Route closures, delays and broadcasts](changes/add-route-alerts/proposal.md) | Admin closes a route; affected users see delay and alerts; broadcast works. | 3 |
| 6 | [Shipment photo upload](changes/add-shipment-documents/proposal.md) | Driver uploads a photo; owner can view it privately. | 2 |
| 7 | [Offline status and location queue](changes/add-offline-updates/proposal.md) | Offline updates survive refresh and automatically sync once. | 4, 5 |
| 8 | [Deployed prototype and presentation](changes/prepare-live-demo/proposal.md) | Deployed demo and timed presentation pass rehearsal. | 1, 2, 3, 4, 5, 6, 7 |

## Confirmed decisions and source conflicts

- **User confirmed:** route closure automatically marks affected shipments DELAYED; reconnect automatically synchronizes queued updates, with manual Retry on failure.
- **Preserve progress during route delay:** show DELAYED while the route is closed, alongside the underlying operational stage. A queued checkpoint can be saved without hiding the route warning. Reopening removes route-induced delay; it does not clear a driver-reported delay. This is the proposed technical interpretation of the confirmed behavior.
- **Required photos and mobile Driver view:** README explicitly requires these, so they remain required even though PRD §52 calls them should-have.
- **Driver selection:** follow PRD §56, where the request creator selects a Driver. The earlier conversations/understanding.md suggestion of Admin dispatch is not an extra required workflow.
- **Customs:** an explicit border-crossing choice controls availability; arriving at Muse alone does not require customs.
- **Admin broadcasts:** included because README requires them, in addition to automatically targeted alerts.
- **Offline scope:** a loaded-page simulation and persistent status/location queue. Cold-start offline navigation, map tile caching and offline photo upload are outside this prototype.

## Shared acceptance conventions

Unless a scenario explicitly states otherwise, use an authenticated authorized actor, an OPEN route, a non-delivered shipment at a valid starting lifecycle stage and a healthy connection. Negative scenarios deliberately override those conditions. Use at least two Traders and two Drivers to check isolation.

Proposed measurable defaults: live changes appear within five seconds after successful server save on a healthy connection; photos accept JPEG/PNG/WebP up to 5 MiB; Driver controls are checked at a 390px viewport. These are planning defaults, not existing implementation guarantees.

The lifecycle field records operational progress; the visible status and delayed counts also include route-induced delay once change 5 is applied. Main specs remain empty until changes are implemented and archived. Cross-change dependencies are documented, not automatically enforced by OpenSpec's per-change artifact status.

## PRD coverage

| Requirement group | Owning changes |
| --- | --- |
| Authentication, role routing, backend authorization (§§6–8, 35, 37) | 1, with resource policies added in 2–7 |
| Shipment fields, lists, ownership, driver selection (§§9–12, 28–32, 56) | 2 |
| Lifecycle, optional customs, timeline, Admin counts (§§13–15, 32, 50) | 3 |
| GPS simulation, map, realtime tracking (§§16–19, 36) | 4 |
| Routes, gate closure, delay alerts, severity, Admin broadcast (§§20–24, 33) | 5 |
| Photos and storage (§§27, 34) | 6 |
| Offline indicator, local queue, synchronization (§§25–26) | 7 |
| Deployment, complete journeys, AI reflection, presentation (§§39–46, 54–55) | 8 and per-feature verification/evidence tasks |
| Stack, page/component organization (§§28–38, 47–48) | Designs and tasks across 1–8 |

Deferred: filtering, advanced search, extended alert history, analytics, charts, route history, ETA, fleet/dispatch management and real GPS. Illustrative routes are demo fixtures, not claims about current road or gate conditions. The PRD roadmap's existing checkmarks do not demonstrate that architecture or code has been implemented.

## Definition of done for each change

1. Complete its tasks and verify every acceptance scenario, including direct backend permission checks where relevant.
2. Record actual AI prompts, failures, fixes and verification evidence in docs/ai-engineering-log.md during implementation.
3. Confirm the slice works with its dependencies and the existing demo flow still works.
4. Archive only after implementation and verification; then its delta becomes an implemented main spec.

## Start implementation

Ask the assistant: **Apply add-role-access.** Work through the remaining changes in dependency order.

Validate planning artifacts with: `openspec validate --all --strict`. This checks OpenSpec structure; it does not execute acceptance scenarios or prove the application works.

