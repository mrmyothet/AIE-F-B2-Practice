## Why

The demo needs a visible truck moving through predefined locations while the trader and administrator watch without refreshing.

## What Changes

- Add predefined simulation points and authorized location updates.
- Display Leaflet maps with shipment markers and route information.
- Show simulation labels and latest update time.

## Capabilities

### New Capabilities

- `live-tracking`: Simulated GPS and map.

### Modified Capabilities

None. This is a new capability; dependent changes are listed below.

## Impact

- Source: PRD §§16–19, 21, 36, 38–39, 47.
- Implement after: `add-shipment-progress`.
- Target: the Next.js application and Supabase services specified in the PRD. Only documents and OpenSpec setup exist today; implementation is proposed.
- Implementation scope and affected components: see design.md and tasks.md.

