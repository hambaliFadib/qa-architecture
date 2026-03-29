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
