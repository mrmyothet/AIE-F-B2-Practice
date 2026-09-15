## Context

See proposal.md for scope and source sections. The repository currently contains the assignment, PRD and OpenSpec tooling, with no application implementation or tests. These are proposed designs using the PRD's Next.js/TypeScript/Tailwind, Supabase, Leaflet/OpenStreetMap and Vercel stack.

Implement after: `add-live-tracking`, `add-route-alerts`.

## Goals / Non-Goals

**Goals:** Deliver the observable scenarios in specs/offline-updates/spec.md as a working, verifiable slice.

**Non-Goals:** Features owned by later changes; payments, real GPS hardware, route optimization, full customs/document management and analytics. No application code is part of this planning change.

## Decisions

1. Use IndexedDB for structured per-user queue entries: operation ID, shipment, action, payload, observed version, capture time and sequence. localStorage is simpler but less suitable for transactional queue changes. Persist before reporting an update as pending.

2. Simulate offline by preventing shipment network writes and realtime delivery to the Driver while retaining already loaded data. This is a loaded-page simulation, not a promise of cold-start offline navigation or cached map tiles. Photos stay online-only.

3. Replay in capture order through existing authenticated status/location operations. Keep each item's stable operation ID until acknowledgement; use returned versions to chain queued operations. Automatic sync starts on restored connectivity or toggling Online, with a single sync worker and manual Retry. Failed items remain queued and success is counted only after server acknowledgement.

4. If other operational progress has advanced, stop that shipment's queue and show a conflict requiring refresh and explicit discard of the stale item. Do not overwrite newer progress or discard data silently. Route closure alone does not invalidate operational progress: replay checkpoints while displaying route delay; a queued delivery is rejected until the route is open.

5. Partition local entries by authenticated account and never submit another account's entries; expired sessions pause sync until the same Driver signs in again. Refreshing the already accessible Driver page preserves the queue. No background service worker or offline photo upload.

## Risks / Trade-offs

- A lost response could replay an update twice → stable operation IDs and server deduplication; changed assignment or progress → pause with visible error instead of overwriting state.
- Proposed acceptance details beyond the PRD (such as the five-second healthy-connection budget and photo size limit where applicable) are prototype defaults for review, not claims about deployed service guarantees.

## Migration Plan

Implement the dependency changes first. Add this slice's schema/policies before the UI that uses them; verify on fresh demo data and run its scenario checks with ordinary user credentials. Keep each slice independently reviewable. If rollout fails, revert the application release and use a forward database correction; preserve shipment/event data and avoid destructive schema rollback. For the initial empty environment, correct and reapply the development setup before loading demo records.

