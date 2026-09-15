## Context

See proposal.md for scope and source sections. The repository currently contains the assignment, PRD and OpenSpec tooling, with no application implementation or tests. These are proposed designs using the PRD's Next.js/TypeScript/Tailwind, Supabase, Leaflet/OpenStreetMap and Vercel stack.

Implement after: `add-shipment-requests`.

## Goals / Non-Goals

**Goals:** Deliver the observable scenarios in specs/shipment-progress/spec.md as a working, verifiable slice.

**Non-Goals:** Features owned by later changes; payments, real GPS hardware, route optimization, full customs/document management and analytics. No application code is part of this planning change.

## Decisions

1. Define transitions in one backend operation: REQUESTED→PICKED_UP; PICKED_UP→IN_TRANSIT; IN_TRANSIT→CHECKPOINT/CUSTOMS/DELAYED/DELIVERED; CHECKPOINT→IN_TRANSIT/CUSTOMS/DELAYED; CUSTOMS→IN_TRANSIT/DELAYED; DELAYED→IN_TRANSIT. CUSTOMS requires crosses_border. DELIVERED is terminal. Route-closure effects are owned by add-route-alerts.

2. Update shipment status and insert an event in a single transaction with authenticated actor, server timestamp and client operation ID. Check expected shipment version to reject stale updates; initialize version in this migration. Offline replay later reuses this command.

3. Use Supabase Realtime with authorized subscriptions and a refetch on reconnect. Proposed demo acceptance budget is five seconds under a healthy connection, measured after successful save.

4. Render actual chronological events, including repeated checkpoints/transit, not a fixed mandatory customs step. Admin counters derive from authorized persisted rows: active means non-DELIVERED, including REQUESTED and DELAYED. Provide driver mobile controls at /driver/shipment.

## Risks / Trade-offs

- Concurrent updates can corrupt status/history → atomic writes, operation deduplication and version checks; realtime loss → refetch current state after reconnect.
- Proposed acceptance details beyond the PRD (such as the five-second healthy-connection budget and photo size limit where applicable) are prototype defaults for review, not claims about deployed service guarantees.

## Migration Plan

Implement the dependency changes first. Add this slice's schema/policies before the UI that uses them; verify on fresh demo data and run its scenario checks with ordinary user credentials. Keep each slice independently reviewable. If rollout fails, revert the application release and use a forward database correction; preserve shipment/event data and avoid destructive schema rollback. For the initial empty environment, correct and reapply the development setup before loading demo records.

