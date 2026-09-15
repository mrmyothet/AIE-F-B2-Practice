## Context

See proposal.md for scope and source sections. The repository currently contains the assignment, PRD and OpenSpec tooling, with no application implementation or tests. These are proposed designs using the PRD's Next.js/TypeScript/Tailwind, Supabase, Leaflet/OpenStreetMap and Vercel stack.

Implement after: `add-shipment-progress`.

## Goals / Non-Goals

**Goals:** Deliver the observable scenarios in specs/route-alerts/spec.md as a working, verifiable slice.

**Non-Goals:** Features owned by later changes; payments, real GPS hardware, route optimization, full customs/document management and analytics. No application code is part of this planning change.

## Decisions

1. Keep shipment lifecycle status as the operational stage; derive the displayed effective status as DELAYED when its route is CLOSED and the shipment is non-DELIVERED. This automatically marks affected shipments delayed without erasing pickup/checkpoint/customs progress. Reopening removes only this route delay; a driver-reported DELAYED stage remains until an authorized resume update. Admin summary counts use effective status. This extends the progress view consistently.

2. Use one authenticated transactional route operation with a request ID. On OPEN→CLOSED, create a route event for each active (non-DELIVERED) shipment and an alerts row per owner/assigned driver, and an Admin-visible activity entry. Repeated CLOSED requests are no-ops; a later reopen/close cycle creates fresh alerts. Serialize shipment creation with route updates so a new request on a closed route is immediately delayed and receives its closure alert.

3. Realtime observers refetch route and effective shipment state on changes; route events do not reset the underlying progress version, allowing queued operational checkpoint updates to replay. Block delivery while the route remains CLOSED; other valid lifecycle updates remain possible and display DELAYED with the underlying stage visible.

4. Driver-reported delay creates an alert for its Trader and an Admin-visible activity entry. Admin broadcasts target all authenticated demo users with normal/warning/high severity; per-recipient alerts keep reads private. /admin/alerts composes messages and reviews activity; other roles see their own alert list. Alert history/search beyond the current list is deferred.

## Risks / Trade-offs

- Offline replay could hide a closure or erase progress → separate effective route delay from lifecycle stage; atomic targeting and request IDs prevent missed or repeated closure alerts.
- Proposed acceptance details beyond the PRD (such as the five-second healthy-connection budget and photo size limit where applicable) are prototype defaults for review, not claims about deployed service guarantees.

## Migration Plan

Implement the dependency changes first. Add this slice's schema/policies before the UI that uses them; verify on fresh demo data and run its scenario checks with ordinary user credentials. Keep each slice independently reviewable. If rollout fails, revert the application release and use a forward database correction; preserve shipment/event data and avoid destructive schema rollback. For the initial empty environment, correct and reapply the development setup before loading demo records.

