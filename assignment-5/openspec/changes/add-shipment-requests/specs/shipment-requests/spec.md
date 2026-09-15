## Purpose

A trader must create a shipment that its assigned driver and administrator can find, while other traders cannot access it.

## ADDED Requirements

### Requirement: Shipment creation

The system SHALL let Traders create their own shipments and Admins create shipments for a selected Trader using cargo, origin, destination, route, driver and an explicit border-crossing choice.

#### Scenario: Valid request

- **WHEN** a Trader submits a complete request with a valid route and Driver
- **THEN** one shipment is created for that Trader with a unique tracking number, REQUESTED status and a timestamped initial event

#### Scenario: Invalid request

- **WHEN** a required value is missing or the selected driver is not a DRIVER
- **THEN** creation is rejected with field feedback and no partial shipment

#### Scenario: Repeated submission

- **WHEN** the same request is submitted again after a retry
- **THEN** the original shipment is returned without a duplicate

#### Scenario: Admin request

- **WHEN** an Admin creates a request for a selected Trader
- **THEN** the selected Trader owns the new shipment

### Requirement: Shipment visibility

The system SHALL let Admins view all shipments, Traders view only their own and Drivers view only assigned shipments.

#### Scenario: Authorized lists

- **WHEN** each role opens its shipment list
- **THEN** only shipments permitted for that role are listed

#### Scenario: Direct access isolation

- **WHEN** another Trader or an unassigned Driver requests a shipment by ID
- **THEN** no shipment details or events are returned

#### Scenario: Driver creation denied

- **WHEN** a Driver submits a shipment creation request
- **THEN** the operation is rejected

### Requirement: Request metadata

The system SHALL show cargo, tracking number, owner, assigned driver, origin, destination, route and status to authorized viewers, and SHALL distinguish domestic transport from actual border crossing.

#### Scenario: Domestic route

- **WHEN** a request is created without international border crossing
- **THEN** its details identify it as domestic even if the destination is Muse

#### Scenario: No assignments

- **WHEN** a Driver with no assigned shipments opens the dashboard
- **THEN** a clear empty state appears
