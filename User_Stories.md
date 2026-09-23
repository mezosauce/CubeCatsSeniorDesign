# Assignment 4 - User Stories and Use Cases

## Stakeholders

| Stakeholder                   | Category  |
| ----------------------------- | --------- |
| Satellite operator            | Primary   |
| Environmental data researcher | Secondary |
| Future club members           | Secondary |
| Amateur radio operator        | Hidden    |

## User Story 1

**US-01 (Primary)**

As a satellite operator,

I want to send authorized commands to HABSat-1 and receive confirmation that the commands were processed,

so that I can control spacecraft operations and verify that the satellite received my instructions.

## User Story 2

**US-02 (Secondary)**

As an environmental data researcher,

I want HABSat-1 to collect multispectral images with their corresponding observation time and mission data,

so that I can use the collected data to analyze harmful algae blooms in the Great Lakes.

## User Story 3

**US-03 (Secondary)**

As a future CubeCats member working on the next satellite mission,

I want to be able to learn from the HABSat-1 flight software documentation and development decisions,

so that I can understand how the previous mission was designed and use that knowledge when developing the next satellite.

## User Story 4

**US-04 (Hidden)**

As a licensed amateur radio operator communicating with HABSat-1,

I want to understand and follow the satellite's communication requirements and procedures,

so that I can communicate with the satellite in accordance with the mission's operating procedures and applicable amateur radio regulations.

# Use Cases

## UC-01 - Send and Process Spacecraft Command

**Story:** US-01

**Primary Actor:** Satellite Operator

**Secondary Actors:** Ground Station, HABSat-1 On-Board Computer (OBC), Satellite Subsystem

### Preconditions

1. HABSat-1's OBC is powered on and the flight software is running.
2. The ground station has an established communication link with HABSat-1.
3. The satellite operator is authorized to send commands to HABSat-1.
4. The command is supported by the flight software.
5. The command is valid for the satellite's current mission flight state.

### Main Success Flow

1. **Satellite Operator:** Selects an authorized command to send to HABSat-1.
2. **Ground Station:** Formats and transmits the command to HABSat-1 using the established communication protocol.
3. **OBC:** Receives the command from the ground station.
4. **OBC:** Validates the command's format, authorization, and compatibility with the current mission flight state.
5. **OBC:** Routes the validated command to the appropriate satellite subsystem.
6. **Satellite Subsystem:** Receives and executes the command.
7. **Satellite Subsystem:** Returns the execution status to the OBC.
8. **OBC:** Records the command and its execution status.
9. **OBC:** Transmits a command confirmation to the ground station.
10. **Ground Station:** Receives the confirmation and makes the command status available to the satellite operator.
11. **Satellite Operator:** Verifies that the command was successfully processed.

### Alternate Flow

**A1: Command is scheduled for later execution**

1. **Satellite Operator:** Sends a valid command with a specified future execution time.
2. **OBC:** Validates the command and verifies that the scheduled execution time is valid.
3. **OBC:** Stores the command in the scheduled task queue.
4. **OBC:** Sends confirmation to the ground station that the command has been accepted for scheduled execution.
5. **OBC:** Waits until the scheduled execution time.
6. **OBC:** Executes the command and sends the execution status to the ground station.

### Exception Flow

**E1: Invalid or unauthorized command**

1. **Satellite Operator:** Sends a command to HABSat-1.
2. **OBC:** Receives the command and determines that the command is malformed, unauthorized, unsupported, or invalid for the current mission flight state.
3. **OBC:** Rejects the command without sending it to the affected subsystem.
4. **OBC:** Sends a command-rejection status to the ground station.
5. **Ground Station:** Presents the rejection status to the satellite operator.

### Postcondition

If the command is valid and successfully executed, the requested spacecraft operation has been performed and the command's execution status has been recorded and reported to the ground station.

If the command is rejected, the requested operation has not been performed and the rejection and reason have been reported to the ground station.

# Acceptance Criteria

## UC-01 Acceptance Criteria

### AC-01.1: Successful Command

**Given** the OBC is running, the ground station has an established communication link, and the satellite operator is authorized to send a command that is valid for the current mission flight state,

**When** the satellite operator sends the command to HABSat-1,

**Then** the OBC shall validate the command, route it to the appropriate subsystem, and provide the ground station with the command's execution status.

### AC-01.2: Invalid Command

**Given** the OBC receives a command that is malformed, unauthorized, unsupported, or invalid for the current mission flight state,

**When** the OBC validates the command,

**Then** the OBC shall reject the command, shall not send it to the affected subsystem, and shall record the reason for rejection.

### AC-01.3: Scheduled Command

**Given** the OBC is running and receives a valid command with a valid future execution time,

**When** the scheduled execution time is reached,

**Then** the OBC shall execute the command and record the resulting execution status.
