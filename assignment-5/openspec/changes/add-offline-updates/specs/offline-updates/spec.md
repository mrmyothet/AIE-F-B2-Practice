## Purpose

The Driver must demonstrate updates during a simulated blackout and recover them without losing or duplicating shipment history.

## ADDED Requirements

### Requirement: Persistent offline capture

The system SHALL allow a Driver with a loaded assigned shipment to queue status and simulated location updates in offline mode, persist them across page refresh, and show the pending count without reporting server success.

#### Scenario: Offline capture

- **WHEN** the Driver toggles Offline and records a checkpoint and location update
- **THEN** two pending items appear and server-side Trader/Admin views remain unchanged

#### Scenario: Refresh pending queue

- **WHEN** the Driver refreshes the accessible application with two queued items
- **THEN** both items and the pending count remain available for that account

### Requirement: Automatic synchronization and retry

The system SHALL automatically send queued updates in capture order when connection returns, remove only acknowledged items, and provide manual retry when synchronization fails.

#### Scenario: Reconnect

- **WHEN** the Driver returns Online with valid queued updates
- **THEN** updates synchronize in order, pending reaches zero and authorized observers see the persisted changes within five seconds of each save

#### Scenario: Lost acknowledgement

- **WHEN** an update reaches the server but its response is lost and the Driver retries
- **THEN** exactly one event exists and the retry acknowledges the original operation

#### Scenario: Network failure

- **WHEN** connectivity fails during synchronization
- **THEN** unsent or unacknowledged items remain pending with a visible retry action

#### Scenario: Manual retry

- **WHEN** the Driver clicks Retry after connectivity is restored
- **THEN** remaining valid items synchronize without resending acknowledged items as new operations

### Requirement: Conflict and account isolation

The system SHALL reject stale or unauthorized queued updates visibly, preserve unresolved items for review, and never synchronize one account's queue as another user.

#### Scenario: Newer progress

- **WHEN** another actor changes operational progress before a queued update synchronizes
- **THEN** sync pauses for that shipment and offers refresh plus explicit discard of the stale item without overwriting newer state

#### Scenario: Expired session

- **WHEN** the Driver's session expires before sync
- **THEN** sync pauses and requests login while preserving queued items

#### Scenario: Account switch

- **WHEN** another Driver logs in on the same browser
- **THEN** the first Driver's queue is neither displayed nor submitted as the second Driver

#### Scenario: Changed assignment

- **WHEN** a queued update belongs to a shipment no longer assigned to the Driver
- **THEN** the server rejects it and the UI retains visible failure feedback

### Requirement: Route closure compatibility

The system SHALL preserve route delay while synchronizing valid underlying progress and SHALL leave a queued delivery unresolved if its route is still closed.

#### Scenario: Checkpoint during closure

- **WHEN** a valid offline checkpoint update synchronizes after Admin closes its route
- **THEN** one checkpoint event is recorded and displayed status remains DELAYED with the closure warning

#### Scenario: Queued delivery blocked

- **WHEN** a delivery update synchronizes while the route is CLOSED
- **THEN** delivery is not recorded and the item remains visibly unresolved for retry after reopening
