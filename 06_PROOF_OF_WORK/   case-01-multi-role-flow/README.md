## 1. Business Context

The system operates within MyTrace, an application designed to manage and monitor task execution for operational teams.

The system supports:

- Task creation (Work Order / WO)
- Task distribution from Admin to Agents
- Task execution by Agents (visit or outbound call)
- Monitoring and reporting by Admin

Example tasks include:

- Field visits (e.g., billing collection, product offering, customer service)
- Outbound calls (e.g., payment reminders, promotions, customer assistance)

The system also includes agent attendance and location tracking to monitor field performance.

The primary business objective is to ensure that assigned tasks are properly executed and traceable from creation to completion.

## 2. Problem Situation

In practice, the system exhibited multiple inconsistencies in coordinating task execution across roles.

Key issues included:

- Work Orders (WO) not appearing on the Agent side after distribution
- Status updates not reflected correctly across roles
- Mismatch between dashboard data and database records
- System dependency on manual data injection to deliver tasks
- Delays in data synchronization affecting task visibility

These issues created a condition where the system could not reliably ensure that tasks were delivered, executed, and reported correctly.

As a result, both operational execution and reporting accuracy were at risk.

## 3. System Flow

The expected multi-role flow is:

1. Admin creates and distributes Work Orders (WO)
2. Agent receives WO
3. Agent performs task execution (Caring), which includes:
   - Visit
   - Outbound Call
4. Agent submits results
5. Admin monitors execution and reviews results
6. Admin generates reports based on task outcomes

This flow represents the core operational cycle for managing field activities.

Each step depends on the successful completion and visibility of the previous step.

## 4. QA Approach

Given the issues observed in the multi-role Work Order flow, the primary QA focus was not limited to whether a WO could be delivered to the Agent.

The main concern was whether the information shown across the system remained accurate and consistent throughout the execution cycle.

### Primary Focus: Data Mismatch and State Inconsistency

The most critical problem was the inconsistency between:

- Dashboard information
- Role-based system views
- Database records

This meant that even if a WO successfully reached the Agent, the process could still fail from a business perspective if the displayed status or reported data did not reflect the actual system state.

### Why This Was the Main QA Focus

For operational systems such as MyTrace, Admin decisions depend on the reliability of monitoring information.

If dashboard values, task counts, or status updates are incorrect, then:

- Admin cannot trust execution visibility
- Field agents may work based on misleading information
- Reporting becomes unreliable
- Operational decisions become risky

Because of this, validating delivery alone was not sufficient.

### QA Strategy

The QA approach prioritized system consistency over superficial flow completion.

This included:

1. Verifying whether state changes were correctly reflected across roles
2. Comparing dashboard information against database records
3. Identifying points where task visibility and reporting became inconsistent
4. Challenging flows that appeared successful operationally but failed in data integrity

### Quality Boundary

The QA position was that a delivered WO should not be considered valid if:

- The status shown to Admin was incorrect
- The dashboard did not match the database
- Monitoring information could not be trusted

In this case, system consistency was treated as a prerequisite for meaningful operational validation.

### Control Objective

The objective was to ensure that the Work Order process was not only executable, but also reliable as a multi-role coordination system.

This means the system must provide:

- Correct state visibility
- Consistent reporting
- Trustworthy operational data

## 5. Control Implementation

To address the identified inconsistencies in the Work Order flow, QA introduced control mechanisms focused on state validation and data integrity.

### Control Points

The following control points were defined across the flow:

1. Distribution Control
   - Verify WO creation in database
   - Validate assignment to Agent
   - Ensure WO visibility in Agent interface

2. Agent Execution Control
   - Validate status transition when Agent starts task
   - Ensure activity (visit/call) updates are persisted in database

3. Monitoring Control (Admin)
   - Compare dashboard data against database records
   - Validate task counts and status aggregation

4. End-to-End State Consistency
   - Track WO lifecycle from creation to completion
   - Identify mismatches between:
     - Database state
     - Agent view
     - Admin dashboard

### Control Objective

The objective of these controls was not to validate UI behavior alone, but to ensure:

- State consistency across all system layers
- Data integrity throughout the process
- Reliable monitoring for business decision-making

### Control Limitation

Due to system instability and lack of clear ownership of state logic:

- Some inconsistencies could be detected but not immediately resolved
- Certain flows could not be validated end-to-end
- Manual intervention (e.g., data injection) reduced traceability

These limitations were explicitly documented as part of QA risk communication.

## 6. System Limitation & Structural Risk

Despite the implemented control mechanisms, several structural risks remained in the system:

### Undefined State Model

The Work Order lifecycle did not have a clearly defined and enforced state machine.

This resulted in:
- Inconsistent state transitions
- Ambiguity in determining the current status of a WO
- Difficulty in validating system behavior reliably

### Lack of State Ownership

There was no clear ownership of state changes:
- Agent actions
- System processes
- Admin interventions

This created conflicts in determining the authoritative source of truth.

### Inconsistent Data Sources

Different system layers (database, dashboard, role-based views) did not consistently reference the same data source.

This led to:
- Data mismatch
- Unreliable monitoring
- Loss of trust in system outputs

### Manual Data Intervention

Manual data injection was used to resolve delivery issues.

However, this introduced:
- Loss of traceability
- Potential data corruption
- Inconsistent system behavior

### QA Position

Given these conditions, QA explicitly recognized that:

- Full validation of system correctness was not achievable
- Only controlled and observable parts of the system could be validated
- Structural issues required resolution at system design level, not testing level
