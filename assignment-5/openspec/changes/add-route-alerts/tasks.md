## 1. Route effects

- [ ] 1.1 Implement route mutation authorization and transactional closure targeting with deduplicated operation IDs; verify forbidden writes, retries and reopen/close cycles.
- [ ] 1.2 Add effective-status projection and retained operational progress to shipment views and Admin counts; verify closure, reopen, manual delay preservation and checkpoint-during-closure cases.
- [ ] 1.3 Serialize request creation against route closure and block delivery on closed routes; verify a newly created affected shipment is delayed/alerted and delivery is rejected.

## 2. Notifications and controls

- [ ] 2.1 Create alerts metadata and recipient access policies; verify direct cross-user alert reads are denied.
- [ ] 2.2 Build /admin/routes and realtime route/effective-status updates; verify correct route fields and five-second propagation.
- [ ] 2.3 Add driver-delay notification and /admin/alerts broadcast composition plus recipient alert lists; verify targeted recipients, empty-message validation and all-user broadcast.
- [ ] 2.4 Run route-alert scenarios across three role sessions and an unrelated Trader; record checks and AI corrections.

