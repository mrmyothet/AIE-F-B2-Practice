## Why

The Driver must demonstrate updates during a simulated blackout and recover them without losing or duplicating shipment history.

## What Changes

- Add a Driver offline toggle and persistent status/location queue.
- Automatically synchronize on reconnection with manual retry for failures.
- Show pending, syncing, synchronized and conflict feedback.

## Capabilities

### New Capabilities

- `offline-updates`: Offline status and location queue.

### Modified Capabilities

None. This is a new capability; dependent changes are listed below.

## Impact

- Source: PRD §§25–26, 43, 47, 56; user-confirmed automatic sync with manual retry.
- Implement after: `add-live-tracking`, `add-route-alerts`.
- Target: the Next.js application and Supabase services specified in the PRD. Only documents and OpenSpec setup exist today; implementation is proposed.
- Implementation scope and affected components: see design.md and tasks.md.

