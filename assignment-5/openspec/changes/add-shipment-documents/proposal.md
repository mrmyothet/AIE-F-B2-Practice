## Why

The assignment explicitly requires the Driver to upload document photos, so this feature remains required despite the PRD's should-have label.

## What Changes

- Provide online document-photo upload for Admin and assigned Driver.
- Store private shipment-linked photo metadata.
- Allow authorized shipment viewers to open uploaded photos.

## Capabilities

### New Capabilities

- `shipment-documents`: Shipment photo upload.

### Modified Capabilities

None. This is a new capability; dependent changes are listed below.

## Impact

- Source: README core Driver requirement; PRD §§6, 27, 34–35, 37, 52.
- Implement after: `add-shipment-requests`.
- Target: the Next.js application and Supabase services specified in the PRD. Only documents and OpenSpec setup exist today; implementation is proposed.
- Implementation scope and affected components: see design.md and tasks.md.

