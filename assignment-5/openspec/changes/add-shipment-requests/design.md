## Context

See proposal.md for scope and source sections. The repository currently contains the assignment, PRD and OpenSpec tooling, with no application implementation or tests. These are proposed designs using the PRD's Next.js/TypeScript/Tailwind, Supabase, Leaflet/OpenStreetMap and Vercel stack.

Implement after: `add-role-access`.

## Goals / Non-Goals

**Goals:** Deliver the observable scenarios in specs/shipment-requests/spec.md as a working, verifiable slice.

**Non-Goals:** Features owned by later changes; payments, real GPS hardware, route optimization, full customs/document management and analytics. No application code is part of this planning change.

## Decisions

1. Use routes and shipments tables from the PRD, with foreign keys to profiles. Add crosses_border boolean because a destination near a border does not itself imply customs. Initially status is REQUESTED and coordinates are empty.

2. Follow PRD §56: the Trader selects a seeded driver on the request form. Admin can create on behalf of a selected trader. Expose only driver ID/name through a restricted directory; do not expose driver email or all profiles. No dispatch/reassignment workflow in this slice.

3. Insert a shipment and its initial shipment_events record atomically through a validated operation. Bind trader ownership to the authenticated user unless the caller is Admin; use a unique constraint and request key to avoid double-submit duplicates.

4. Build /trader/request, /trader/shipments, /trader/shipments/[id], /admin/shipments and the assigned-shipment list at /driver. /driver/shipment selects an authorized assigned shipment. Reuse a detail view and show a clear empty state.

## Risks / Trade-offs

- Client-supplied owner or driver IDs could bypass authorization → validate ownership and DRIVER role on the backend; test a second trader and driver.
- Proposed acceptance details beyond the PRD (such as the five-second healthy-connection budget and photo size limit where applicable) are prototype defaults for review, not claims about deployed service guarantees.

## Migration Plan

Implement the dependency changes first. Add this slice's schema/policies before the UI that uses them; verify on fresh demo data and run its scenario checks with ordinary user credentials. Keep each slice independently reviewable. If rollout fails, revert the application release and use a forward database correction; preserve shipment/event data and avoid destructive schema rollback. For the initial empty environment, correct and reapply the development setup before loading demo records.

