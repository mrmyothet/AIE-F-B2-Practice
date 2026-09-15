## Purpose

Admins must simulate a route closure and affected users must immediately understand its impact without notifying unrelated shipments.

## ADDED Requirements

### Requirement: Admin route control

The system SHALL let only Admins toggle illustrative routes OPEN/CLOSED and show route name, origin, destination, description and last update time.

#### Scenario: Close route

- **WHEN** an Admin closes the OPEN Muse route
- **THEN** it is saved as CLOSED with a new update time

#### Scenario: Unauthorized change

- **WHEN** a Trader or Driver attempts the same operation directly
- **THEN** it is rejected without changing the route

### Requirement: Automatic route delay

The system SHALL display non-delivered shipments on CLOSED routes as DELAYED while retaining their underlying lifecycle progress, and SHALL prevent delivery until the route reopens.

#### Scenario: Affected shipments

- **WHEN** Muse closes while one shipment is IN_TRANSIT on Muse, another is on Myawaddy and a third is already DELIVERED on Muse
- **THEN** only the active Muse shipment becomes effectively DELAYED and its transit stage is retained

#### Scenario: Progress during closure

- **WHEN** a delayed-by-route shipment records a valid checkpoint update
- **THEN** the checkpoint appears in history while the main status remains DELAYED and the closed-route warning remains visible

#### Scenario: Reopen

- **WHEN** Admin reopens the route
- **THEN** route-induced delay disappears and retained progress is shown; driver-reported delays remain DELAYED

#### Scenario: Delivery on closed route

- **WHEN** a Driver attempts to mark a shipment DELIVERED while its route is CLOSED
- **THEN** delivery is rejected with a route-closed explanation

#### Scenario: Request on closed route

- **WHEN** a Trader creates a shipment on a CLOSED route
- **THEN** the new shipment retains REQUESTED progress but displays DELAYED with the route warning

### Requirement: Targeted closure alerts

The system SHALL notify each affected shipment's Trader and assigned Driver within five seconds on a healthy connection and SHALL avoid duplicate alerts for a repeated closure operation.

#### Scenario: Correct recipients

- **WHEN** Admin closes Muse with Trader A assigned to an active Muse shipment and Trader B assigned only to Myawaddy
- **THEN** Trader A and the Muse Driver receive a shipment-linked closure alert within five seconds without refresh; Trader B receives none for that closure

#### Scenario: Closure retry

- **WHEN** the closure operation is retried or CLOSED is set again without reopening
- **THEN** no duplicate closure events or alerts are created

#### Scenario: New closure cycle

- **WHEN** Admin reopens and then closes Muse again
- **THEN** affected users receive a new closure alert

#### Scenario: New affected request

- **WHEN** a shipment is created on an already CLOSED route
- **THEN** its Trader and Driver receive the closure alert

### Requirement: Delay alerts and broadcasts

The system SHALL notify the owning Trader of a driver-reported delay, let Admins broadcast nonempty messages with severity to all demo users, and restrict recipient alerts to their owners and Admins.

#### Scenario: Driver delay notification

- **WHEN** the assigned Driver records a new DELAYED lifecycle stage
- **THEN** the Trader receives a delay alert within five seconds and Admin sees the activity

#### Scenario: Broadcast

- **WHEN** Admin sends a warning broadcast
- **THEN** all demo users receive the message with warning severity without refresh

#### Scenario: Empty or unauthorized broadcast

- **WHEN** an empty message or a non-Admin broadcast request is submitted
- **THEN** it is rejected

#### Scenario: Alert privacy

- **WHEN** one Trader requests another Trader's alert
- **THEN** access is denied

### Requirement: Admin disruption summary

The system SHALL show closed-route count and recent alert activity and count route-affected shipments as delayed.

#### Scenario: Closed-route summary

- **WHEN** Muse is CLOSED and one otherwise IN_TRANSIT shipment uses it
- **THEN** Admin sees one closed route and that shipment is included in the delayed count
