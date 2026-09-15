## Purpose

The demo needs a visible truck moving through predefined locations while the trader and administrator watch without refreshing.

## ADDED Requirements

### Requirement: Simulated location updates

The system SHALL let Admins and assigned Drivers move a non-delivered shipment through predefined route locations while preserving shipment status.

#### Scenario: Next waypoint

- **WHEN** the assigned Driver selects Update Location
- **THEN** the next route location and timestamp are saved, one location event is added and shipment status is unchanged

#### Scenario: Unauthorized location

- **WHEN** another Driver or a Trader submits coordinates directly
- **THEN** the update is denied

#### Scenario: End of route

- **WHEN** the shipment is at its final simulation point
- **THEN** the next-location control cannot move it past the route

#### Scenario: Invalid or duplicate operation

- **WHEN** an invalid coordinate is submitted or a successful operation ID is retried
- **THEN** invalid data is rejected and retries do not create duplicate events

### Requirement: Live map visibility

The system SHALL show shipment markers only to authorized viewers and update their positions within five seconds of a successful location save on a healthy connection.

#### Scenario: Live movement

- **WHEN** a Driver updates location with Admin and owning Trader views open
- **THEN** their markers move within five seconds without a page refresh

#### Scenario: Map isolation

- **WHEN** a different Trader opens the map or requests location data
- **THEN** the other Trader's shipment coordinates are not exposed

### Requirement: Honest simulation display

The system SHALL identify GPS positions as simulated, show latest update time and route information, and handle unavailable locations or map tiles visibly.

#### Scenario: No coordinates

- **WHEN** a shipment has no recorded position
- **THEN** the map area explains that location is not yet available

#### Scenario: Tile failure

- **WHEN** map tiles fail to load
- **THEN** shipment status and readable latest location remain accessible with map failure feedback

#### Scenario: Simulation identification

- **WHEN** a shipment has a recorded simulated position
- **THEN** the view labels it simulated and displays the last update time
