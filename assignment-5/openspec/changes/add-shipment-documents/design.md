## Context

See proposal.md for scope and source sections. The repository currently contains the assignment, PRD and OpenSpec tooling, with no application implementation or tests. These are proposed designs using the PRD's Next.js/TypeScript/Tailwind, Supabase, Leaflet/OpenStreetMap and Vercel stack.

Implement after: `add-shipment-requests`.

## Goals / Non-Goals

**Goals:** Deliver the observable scenarios in specs/shipment-documents/spec.md as a working, verifiable slice.

**Non-Goals:** Features owned by later changes; payments, real GPS hardware, route optimization, full customs/document management and analytics. No application code is part of this planning change.

## Decisions

1. Use a private Supabase Storage bucket and documents metadata linked to shipment and uploader. Store an object path rather than a permanent public URL; create short-lived authorized URLs for viewing. Preserve driver_id for the assigned driver and add uploaded_by to correctly represent Admin uploads.

2. Proposed prototype limits: JPEG/PNG/WebP images up to 5 MiB, with a selected type (delivery, cargo, checkpoint, other). Validate both client feedback and storage/backend limits. Use an upload ID for retry deduplication; clean up an uploaded object when metadata saving fails.

3. Implement /driver/documents and a shared shipment document list. Online uploads only; offline status/location caching is a separate capability, so the offline upload control explains that a connection is required. No OCR, PDF management or offline photo queue.

## Risks / Trade-offs

- A private photo could be exposed by a public URL → private bucket policies and authorized URL issuance; partial upload failure → cleanup and clear retry feedback.
- Proposed acceptance details beyond the PRD (such as the five-second healthy-connection budget and photo size limit where applicable) are prototype defaults for review, not claims about deployed service guarantees.

## Migration Plan

Implement the dependency changes first. Add this slice's schema/policies before the UI that uses them; verify on fresh demo data and run its scenario checks with ordinary user credentials. Keep each slice independently reviewable. If rollout fails, revert the application release and use a forward database correction; preserve shipment/event data and avoid destructive schema rollback. For the initial empty environment, correct and reapply the development setup before loading demo records.

