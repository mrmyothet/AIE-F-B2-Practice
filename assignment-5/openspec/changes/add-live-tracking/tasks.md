## 1. Location service

- [ ] 1.1 Add illustrative waypoint fixtures and atomic location updates using version and operation IDs; verify next-point, invalid-coordinate and retry behavior.
- [ ] 1.2 Enforce assignment and delivered-state checks; verify unauthorized and delivered-shipment writes are denied.

## 2. Tracking UI

- [ ] 2.1 Implement client-only TrackingMap with attribution, route details and simulation timestamp; verify known coordinates and empty/error states.
- [ ] 2.2 Add driver next-location controls and role-scoped map views; verify final-waypoint behavior and location privacy.
- [ ] 2.3 Wire realtime and reconnect refetch; verify Admin/Trader map movement within five seconds in separate sessions and record the result in the AI log.

