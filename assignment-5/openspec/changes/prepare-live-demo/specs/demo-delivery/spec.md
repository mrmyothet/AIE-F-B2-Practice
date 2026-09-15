## Purpose

The assignment is complete only when the integrated prototype is accessible for a reliable live demonstration and the team can explain its AI engineering work.

## ADDED Requirements

### Requirement: Live prototype access

The prototype SHALL be available at a documented HTTPS URL and support seeded Admin, Trader and Driver login with enforced role permissions.

#### Scenario: Deployed access

- **WHEN** a reviewer opens the documented URL and signs in with each supplied demo role
- **THEN** the expected role view opens and authorized shipment operations work

#### Scenario: Production isolation

- **WHEN** a demo Trader attempts to access another Trader's shipment on the deployed app
- **THEN** access is denied

### Requirement: Repeatable demonstration

The prototype SHALL support a rehearsed end-to-end demonstration of request creation, driver progress, simulated tracking, photo upload, route closure alerts, offline recovery, reopening and delivery.

#### Scenario: Full rehearsal

- **WHEN** the team follows the documented demo script from its prepared fixture state
- **THEN** all three roles demonstrate the complete flow within the allotted 15-minute demo segment

#### Scenario: Driver mobile view

- **WHEN** the Driver performs shipment actions at a 390px viewport
- **THEN** status, location, photo and offline controls are visible and usable without horizontal scrolling

### Requirement: Presentation evidence

The team SHALL prepare a 30-minute presentation with 5 minutes for problem/solution, 15 for live demo and 10 for AI engineering reflection using recorded prompts, failures, corrections and validation.

#### Scenario: Presentation readiness

- **WHEN** the team rehearses the prepared presentation
- **THEN** each required segment and concrete AI engineering evidence is present and fits its time allocation
