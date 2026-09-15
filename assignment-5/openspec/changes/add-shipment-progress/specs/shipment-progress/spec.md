## Purpose

The shipment needs a demonstrable lifecycle with checkpoint, delay and conditional customs history that all authorized roles can follow.

## ADDED Requirements

### Requirement: Authorized progress

The system SHALL allow only Admins and the assigned Driver to advance shipment status through valid transitions and SHALL record each successful change once.

#### Scenario: Domestic delivery

- **WHEN** the Driver advances REQUESTED → PICKED_UP → IN_TRANSIT → CHECKPOINT → IN_TRANSIT → DELIVERED
- **THEN** each step succeeds with one ordered event and no required CUSTOMS step

#### Scenario: Driver delay

- **WHEN** the Driver marks an IN_TRANSIT shipment DELAYED and later IN_TRANSIT
- **THEN** both changes are recorded in its history

#### Scenario: Unauthorized update

- **WHEN** a Trader or unassigned Driver attempts to update status directly
- **THEN** the request is denied without changing status or history

#### Scenario: Invalid or stale update

- **WHEN** an update skips from REQUESTED to DELIVERED or uses an outdated shipment version
- **THEN** the operation is rejected and current persisted state is returned for refresh

#### Scenario: Duplicate operation

- **WHEN** a previously successful status operation is retried with the same operation ID
- **THEN** the original result is returned without another event

### Requirement: Conditional customs

The system SHALL permit CUSTOMS only for shipments explicitly marked as crossing an international border.

#### Scenario: Border customs

- **WHEN** a border-crossing shipment moves from CHECKPOINT to CUSTOMS then IN_TRANSIT
- **THEN** the updates succeed and customs appears in history

#### Scenario: Domestic customs rejected

- **WHEN** a domestic shipment requests CUSTOMS
- **THEN** the update is rejected

### Requirement: Live timeline and completion

The system SHALL display status, time, location when known and optional description in chronological history, update authorized views within five seconds of a successful save on a healthy connection, and prevent progress changes after delivery.

#### Scenario: Live history

- **WHEN** a Driver saves a checkpoint update while the owning Trader and Admin have the shipment open
- **THEN** both see the new status and event within five seconds without refresh

#### Scenario: Terminal delivery

- **WHEN** a status change is submitted for a delivered shipment
- **THEN** it is rejected and delivery history remains unchanged

### Requirement: Admin summary

The system SHALL show total, active, delayed and delivered shipment counts, where active includes every non-delivered shipment.

#### Scenario: Known counts

- **WHEN** Admin views data containing one REQUESTED, one DELAYED and one DELIVERED shipment
- **THEN** total is 3, active is 2, delayed is 1 and delivered is 1
