## Why

The shipment needs a demonstrable lifecycle with checkpoint, delay and conditional customs history that all authorized roles can follow.

## What Changes

- Add validated driver/admin status updates and timestamped history.
- Show a chronological shipment timeline and live status changes.
- Provide Admin shipment summary counts.

## Capabilities

### New Capabilities

- `shipment-progress`: Status updates and timeline.

### Modified Capabilities

None. This is a new capability; dependent changes are listed below.

## Impact

- Source: PRD §§13–15, 32, 40–43, 50, 56.
- Implement after: `add-shipment-requests`.
- Target: the Next.js application and Supabase services specified in the PRD. Only documents and OpenSpec setup exist today; implementation is proposed.
- Implementation scope and affected components: see design.md and tasks.md.

