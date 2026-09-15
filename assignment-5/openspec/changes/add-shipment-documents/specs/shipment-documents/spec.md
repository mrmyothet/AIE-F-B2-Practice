## Purpose

The assignment explicitly requires the Driver to upload document photos, so this feature remains required despite the PRD's should-have label.

## ADDED Requirements

### Requirement: Authorized photo upload

The system SHALL allow Admins and assigned Drivers to upload JPEG, PNG or WebP shipment photos up to 5 MiB with a document type, and SHALL reject other users or invalid files.

#### Scenario: Driver upload

- **WHEN** an assigned Driver uploads a valid checkpoint photo online
- **THEN** the photo and its filename, shipment, uploader, type and upload time appear in that shipment's document list

#### Scenario: Admin upload

- **WHEN** an Admin uploads a valid photo for a shipment
- **THEN** the Admin is recorded as uploader

#### Scenario: Forbidden upload

- **WHEN** a Trader or unassigned Driver uploads to a shipment directly
- **THEN** the upload is rejected

#### Scenario: Invalid photo

- **WHEN** a file exceeds 5 MiB or is not an allowed image type
- **THEN** the upload is rejected with feedback and no document entry

### Requirement: Private document access

The system SHALL allow document viewing only for Admins, the owning Trader and assigned Driver.

#### Scenario: Authorized viewing

- **WHEN** the owning Trader opens an uploaded document
- **THEN** the photo is displayed

#### Scenario: Private storage

- **WHEN** another Trader requests the document or its storage object
- **THEN** access is denied

### Requirement: Upload recovery

The system SHALL display upload progress, success or failure, prevent duplicate records on retry, and require an online connection for photo upload.

#### Scenario: Offline upload

- **WHEN** the Driver's connection is unavailable
- **THEN** photo upload is unavailable and explains that a connection is required

#### Scenario: Failed metadata save

- **WHEN** the file upload succeeds but saving its document record fails
- **THEN** failure is shown and no broken document entry is presented

#### Scenario: Retry

- **WHEN** a successful upload is retried with the same upload identifier
- **THEN** only one document entry exists
