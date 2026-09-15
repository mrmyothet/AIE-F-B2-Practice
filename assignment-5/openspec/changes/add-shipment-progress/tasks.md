## 1. Progress contract

- [ ] 1.1 Add version and operation-ID support and the atomic status transition operation; verify domestic, border, invalid, stale and duplicate cases.
- [ ] 1.2 Enforce Admin/assigned-Driver access for status writes and event reads; verify forged direct requests cannot mutate another shipment.

## 2. Views and integration

- [ ] 2.1 Build driver status controls and the chronological ShipmentTimeline; verify repeated checkpoint/transit entries and conditional customs.
- [ ] 2.2 Subscribe authorized detail views to persisted changes and refetch on reconnect; verify separate Trader/Admin sessions update within five seconds.
- [ ] 2.3 Add Admin summary counts; verify the three-shipment count fixture.
- [ ] 2.4 Run the full shipment-progress scenarios and record AI corrections; verify delivery is terminal and a rejected update adds no event.

