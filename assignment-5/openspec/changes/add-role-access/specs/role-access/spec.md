## Purpose

All three demo users need authenticated access and reliable separation of their data before shipment features can be built.

## ADDED Requirements

### Requirement: Role-based login

The system SHALL authenticate users and direct ADMIN, TRADER and DRIVER users to their respective dashboards.

#### Scenario: Valid login

- **WHEN** each seeded role logs in with valid credentials
- **THEN** the corresponding /admin, /trader or /driver page opens

#### Scenario: Invalid login

- **WHEN** a user submits invalid credentials
- **THEN** an error is shown and protected content remains inaccessible

### Requirement: Protected sessions

The system SHALL require a valid session for protected pages and data, and remove access on logout.

#### Scenario: Anonymous access

- **WHEN** a logged-out user opens a protected URL or requests protected data directly
- **THEN** the page redirects to login and the data request is denied

#### Scenario: Logout

- **WHEN** a logged-in user logs out and revisits a protected page
- **THEN** login is required again

### Requirement: Role enforcement

The system SHALL enforce the user's trusted role on the backend and prevent self-promotion.

#### Scenario: Wrong role

- **WHEN** a Trader opens an Admin URL or invokes an Admin-only operation directly
- **THEN** access is denied

#### Scenario: Self-promotion

- **WHEN** a Trader attempts to update their role to ADMIN through a direct request
- **THEN** the change is rejected and the stored role remains TRADER
