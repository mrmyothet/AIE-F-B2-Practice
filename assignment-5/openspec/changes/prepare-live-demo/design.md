## Context

See proposal.md for scope and source sections. The repository currently contains the assignment, PRD and OpenSpec tooling, with no application implementation or tests. These are proposed designs using the PRD's Next.js/TypeScript/Tailwind, Supabase, Leaflet/OpenStreetMap and Vercel stack.

Implement after: `add-role-access`, `add-shipment-requests`, `add-shipment-progress`, `add-live-tracking`, `add-route-alerts`, `add-shipment-documents`, `add-offline-updates`.

## Goals / Non-Goals

**Goals:** Deliver the observable scenarios in specs/demo-delivery/spec.md as a working, verifiable slice.

**Non-Goals:** Features owned by later changes; payments, real GPS hardware, route optimization, full customs/document management and analytics. No application code is part of this planning change.

## Decisions

1. Deploy the Next.js app to Vercel against a dedicated demo Supabase project using environment-provided configuration. Document the deployment URL and migration order; never put a service-role key in a browser bundle.

2. Use explicit seed/reset tooling confined to the demo environment. Prepare at least two traders, two drivers, three illustrative routes and active/delivered fixtures so negative recipient and permission checks are reproducible. Require an explicit demo-target argument before resetting data; do not expose a public reset endpoint.

3. Document the 15-minute live script and 5/10-minute surrounding sections. Collect real prompts, failures, fixes and verification during every feature; do not invent retrospective evidence. A backup recording mitigates demo connectivity problems.

4. Verify the integrated application with separate role sessions and representative 390px Driver viewport. Setup/deployment commands and exact dependency versions are selected and checked during implementation against installed tools and official docs; no application code exists yet.

## Risks / Trade-offs

- External service or network failure can disrupt the demo → rehearse the deployed URL and retain a backup recording; mismatched seed state → explicit demo-only reset and preflight checklist.
- Proposed acceptance details beyond the PRD (such as the five-second healthy-connection budget and photo size limit where applicable) are prototype defaults for review, not claims about deployed service guarantees.

## Migration Plan

Implement the dependency changes first. Add this slice's schema/policies before the UI that uses them; verify on fresh demo data and run its scenario checks with ordinary user credentials. Keep each slice independently reviewable. If rollout fails, revert the application release and use a forward database correction; preserve shipment/event data and avoid destructive schema rollback. For the initial empty environment, correct and reapply the development setup before loading demo records.

