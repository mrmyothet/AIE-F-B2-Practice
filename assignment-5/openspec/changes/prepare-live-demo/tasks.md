## 1. Release preparation

- [ ] 1.1 Write docs/architecture.md and docs/database-schema.md from the implemented system; verify they match migrations, permissions and route-delay handling.
- [ ] 1.2 Create explicit demo-only seed/reset tooling and docs/demo-scenario.md with role fixtures, unrelated shipments and expected outcomes; verify reset and a complete local rehearsal.
- [ ] 1.3 Configure Vercel and demo Supabase environments, apply migrations and deploy; verify the HTTPS URL, role logins and absence of privileged keys in browser assets.

## 2. Demo verification

- [ ] 2.1 Run all feature acceptance checks on the deployed environment using separate role sessions; record results and fix failures before marking complete.
- [ ] 2.2 Rehearse tracking, photo upload, route closure, offline checkpoint sync, reopening and delivery at a 390px Driver viewport; verify the live segment fits 15 minutes.
- [ ] 2.3 Prepare the 5/15/10-minute presentation, AI evidence log and backup recording; verify materials reflect actual work and the full rehearsal fits 30 minutes.

