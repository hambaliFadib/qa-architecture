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
