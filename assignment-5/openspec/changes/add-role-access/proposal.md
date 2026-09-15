## Why

All three demo users need authenticated access and reliable separation of their data before shipment features can be built.

## What Changes

- Scaffold the specified Next.js, TypeScript, Tailwind and Supabase application.
- Provide login, logout and role-specific landing pages.
- Seed demo identities and enforce backend authorization.

## Capabilities

### New Capabilities

- `role-access`: Login and role access.

### Modified Capabilities

None. This is a new capability; dependent changes are listed below.

## Impact

- Source: PRD §§6–8, 35, 37, 47; README role requirements.
- Implement after: none; this is the foundation.
- Target: the Next.js application and Supabase services specified in the PRD. Only documents and OpenSpec setup exist today; implementation is proposed.
- Implementation scope and affected components: see design.md and tasks.md.

