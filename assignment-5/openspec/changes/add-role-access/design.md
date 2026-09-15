## Context

See proposal.md for scope and source sections. The repository currently contains the assignment, PRD and OpenSpec tooling, with no application implementation or tests. These are proposed designs using the PRD's Next.js/TypeScript/Tailwind, Supabase, Leaflet/OpenStreetMap and Vercel stack.

Implement after: no dependency.

## Goals / Non-Goals

**Goals:** Deliver the observable scenarios in specs/role-access/spec.md as a working, verifiable slice.

**Non-Goals:** Features owned by later changes; payments, real GPS hardware, route optimization, full customs/document management and analytics. No application code is part of this planning change.

## Decisions

1. Use Supabase Auth and profiles keyed by auth user ID. Roles are ADMIN, TRADER and DRIVER, assigned by trusted seed/admin tooling; client profile edits cannot change roles. This avoids building custom password storage.

2. Use server-verified sessions and PostgreSQL row-level security together. Page guards provide navigation; backend policies enforce data access even for direct requests. Later changes add policies for their own resources.

3. Create app/login and role layouts, lib/supabase browser/server clients, migrations and a repeatable demo seed. Seed two traders and two drivers for isolation checks, plus one admin. Keep credentials outside tracked files. Use simple mobile navigation and large driver buttons; no registration or role-management UI.

## Risks / Trade-offs

- Session or policy errors could expose data → test direct unauthenticated requests and attempts to change roles, not only hidden buttons.
- Proposed acceptance details beyond the PRD (such as the five-second healthy-connection budget and photo size limit where applicable) are prototype defaults for review, not claims about deployed service guarantees.

## Migration Plan

Implement the dependency changes first. Add this slice's schema/policies before the UI that uses them; verify on fresh demo data and run its scenario checks with ordinary user credentials. Keep each slice independently reviewable. If rollout fails, revert the application release and use a forward database correction; preserve shipment/event data and avoid destructive schema rollback. For the initial empty environment, correct and reapply the development setup before loading demo records.

