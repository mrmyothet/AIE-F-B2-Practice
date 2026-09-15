## Context

See proposal.md for scope and source sections. The repository currently contains the assignment, PRD and OpenSpec tooling, with no application implementation or tests. These are proposed designs using the PRD's Next.js/TypeScript/Tailwind, Supabase, Leaflet/OpenStreetMap and Vercel stack.

Implement after: `add-shipment-progress`.

## Goals / Non-Goals

**Goals:** Deliver the observable scenarios in specs/live-tracking/spec.md as a working, verifiable slice.

**Non-Goals:** Features owned by later changes; payments, real GPS hardware, route optimization, full customs/document management and analytics. No application code is part of this planning change.

## Decisions

1. Use Leaflet with OpenStreetMap in a client-only TrackingMap component because map rendering requires browser APIs. Retain visible map attribution. Use predefined illustrative coordinates keyed by route; do not imply real route operating conditions.

2. Reuse the shipment version/operation-ID pattern to atomically save coordinates and a location event without changing status. Coordinate validation and assignment checks run on the backend. Keep location updates distinct from status transitions in event metadata.

3. Provide next-location controls and a stop at the final waypoint. Render all active shipment markers on Admin and only authorized markers on Trader/Driver views. A missing location produces an explicit empty state rather than a fabricated coordinate.

4. Use authorized Supabase Realtime subscriptions and reconnect refetch, with the same five-second healthy-connection demo budget. Keep map loading failures separate from shipment details so status information remains usable.

## Risks / Trade-offs

- External map tiles may be unavailable during the demo → show readable coordinates/latest location and an error state; prepare a backup recording in the release checklist.
- Proposed acceptance details beyond the PRD (such as the five-second healthy-connection budget and photo size limit where applicable) are prototype defaults for review, not claims about deployed service guarantees.

## Migration Plan

Implement the dependency changes first. Add this slice's schema/policies before the UI that uses them; verify on fresh demo data and run its scenario checks with ordinary user credentials. Keep each slice independently reviewable. If rollout fails, revert the application release and use a forward database correction; preserve shipment/event data and avoid destructive schema rollback. For the initial empty environment, correct and reapply the development setup before loading demo records.

