## 1. Data and creation

- [ ] 1.1 Create routes, shipments and initial shipment_events migrations with foreign keys, ownership policies and request deduplication; verify fresh migration and repeat-request behavior.
- [ ] 1.2 Seed illustrative Muse, Myawaddy and domestic routes and add a restricted driver directory; verify Traders see driver names without private profile data.
- [ ] 1.3 Build validated shipment creation for Trader and Admin in lib/services and request forms; verify invalid fields and forged owner/driver IDs are rejected.

## 2. Role views

- [ ] 2.1 Build role-scoped lists, details and driver assignment selection; verify two-trader/two-driver isolation through UI and direct data requests.
- [ ] 2.2 Render shipment metadata and domestic/border choice; verify empty assignments and creation feedback.
- [ ] 2.3 Run shipment-request scenarios end to end and log an AI generation/review example; verify one request is visible to its owner, assigned Driver and Admin only.

