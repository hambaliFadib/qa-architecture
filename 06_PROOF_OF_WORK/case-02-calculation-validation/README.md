## 1. Business Context

The system operates within the PGN Energy platform, specifically in the RBI (Rating, Billing, Invoice) module.

This module is responsible for calculating gas consumption based on measured usage tied to customer Service Agreements (SA).

The calculation result directly impacts:

- Customer billing amounts
- Financial reporting
- Regulatory compliance

Therefore, accuracy and consistency in calculation logic are critical to ensure trust and correctness in the business process.

## 2. Problem Situation

In practice, the calculation system operates under unstable and unclear conditions.

Several critical issues were observed:

- Calculation results did not align with expected business logic
- System failures occurred despite valid data (e.g., "SA not found" while SA is active)
- Gas source determination logic was unclear and inconsistent
- Rule hierarchy (e.g., BAGP, KEPMEN, MAIN) was not explicitly defined
- Multiple adjustment mechanisms existed without clear boundaries

These conditions created a high risk of incorrect billing and system inconsistency.

## 3. System Flow

The expected calculation flow in the system is:

1. Usage Upload
2. Pre-Billing Process
3. Rating Calculation
4. Billing Calculation
5. Invoice Generation
6. Delivery Management

In some scenarios, rating and billing calculations can be executed separately or combined.

This flow represents the core process for generating customer invoices based on gas consumption.

## 4. QA Approach

Given the unstable and ambiguous nature of the calculation module, the primary QA focus was not to validate every complex rule immediately, but to first establish consistency in the core calculation flow.

The main approach taken was to prioritize system consistency over rule expansion.

### Primary Focus: System Inconsistency

The most critical issue was not only incorrect formulas, but the fact that the system could not consistently execute business-critical happy paths.

Examples included:

- Active Service Agreements being treated as not found
- System states appearing successful in the UI while backend execution failed
- Core processing flow becoming unreliable despite valid prerequisite data

This created a condition where deeper rule validation became unreliable, because the foundation of the process itself was unstable.

### QA Strategy

The QA approach was focused on securing the minimum business-critical path first:

1. Ensure that the core flow can run consistently:
   - Usage Upload
   - Rating Calculation
   - Billing Calculation
   - Invoice Generation

2. Challenge any failure in the happy path that lacked a clear business explanation

3. Separate “system inconsistency” issues from “complex business rule” issues

4. Prevent the team from normalizing broken system behavior as acceptable simply because it already existed

### Why This Approach Was Chosen

In a highly ambiguous project, validating advanced rules without first stabilizing the core flow would create false confidence.

For that reason, QA prioritized:

- Explainable execution
- Stable processing behavior
- Traceable failure points

Only after the system could reliably execute the business-critical happy path would further rule-level validation become meaningful.

### Control Objective

The objective was not merely to confirm that calculations produced output, but to ensure that the system behaved consistently enough to be trusted as a business processing engine.

## 5. Control Implementation

To manage system inconsistency in the calculation module, QA implemented a structured control system rather than relying on isolated testing activities.

### QA Log as Central Control

The QA Log was used as the primary control mechanism to track:

- Test execution results
- Identified inconsistencies
- Validation outcomes across the calculation flow

Each entry was not treated as an isolated defect, but as part of a broader system context, linking:

- Business flow stage (usage, rating, billing)
- System module involved
- Observed behavior vs expected behavior

This allowed QA to detect patterns rather than isolated issues.

### Mapping to Business Flow

All findings were mapped back to the core calculation flow:

- Usage Upload
- Rating Calculation
- Billing Calculation
- Invoice Generation

This ensured that inconsistencies were understood in relation to their impact on the overall business process, not just at the technical level.

### DEV Work Synchronization

QA findings were aligned with development tracking through structured DEV Work logs (FE/BE/DB).

This enabled:

- Visibility of implementation changes
- Tracking of issue resolution across layers
- Correlation between system changes and observed behavior

### Calculation Control Layer

A dedicated calculation control structure was used to monitor:

- Input data consistency
- Rule application behavior
- Output validation results

This helped isolate whether inconsistencies originated from:

- Data issues
- Rule misapplication
- System execution failures

### Rhythm Control

Given the unstable nature of the project, QA maintained a rhythm control mechanism to track:

- Iteration cycles
- Repeated issues
- Regression patterns

This prevented the system from repeatedly failing in the same areas without visibility.

---

### Control Objective

The objective of this control system was to transform fragmented observations into a structured and traceable quality view.

Instead of reacting to issues individually, QA established a system-level understanding of:

- Where inconsistencies occur
- How they propagate across the flow
- What their impact is on business outcomes
