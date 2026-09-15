## Why

A trader must create a shipment that its assigned driver and administrator can find, while other traders cannot access it.

## What Changes

- Seed illustrative Muse, Myawaddy and domestic routes.
- Create requests with selected driver and a unique tracking number.
- Provide role-scoped shipment lists and details.

## Capabilities

### New Capabilities

- `shipment-requests`: Create and view assigned shipments.

### Modified Capabilities

None. This is a new capability; dependent changes are listed below.

## Impact

- Source: PRD §§6, 9–12, 28–32, 37, 56.
- Implement after: `add-role-access`.
- Target: the Next.js application and Supabase services specified in the PRD. Only documents and OpenSpec setup exist today; implementation is proposed.
- Implementation scope and affected components: see design.md and tasks.md.

