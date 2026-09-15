## Why

Admins must simulate a route closure and affected users must immediately understand its impact without notifying unrelated shipments.

## What Changes

- Add Admin route open/close controls and automatic shipment delay indication.
- Deliver targeted route and driver-delay alerts in real time.
- Provide Admin broadcast alerts and closed-route/recent-alert dashboard sections.

## Capabilities

### New Capabilities

- `route-alerts`: Route closures, delays and broadcasts.

### Modified Capabilities

None. This is a new capability; dependent changes are listed below.

## Impact

- Source: README Admin/gate requirements; PRD §§20–24, 33, 36, 43, 56; user-confirmed automatic delays.
- Implement after: `add-shipment-progress`.
- Target: the Next.js application and Supabase services specified in the PRD. Only documents and OpenSpec setup exist today; implementation is proposed.
- Implementation scope and affected components: see design.md and tasks.md.

