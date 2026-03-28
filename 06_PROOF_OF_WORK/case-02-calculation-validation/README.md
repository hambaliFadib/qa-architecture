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

## 6. Key Findings

During the validation of the calculation module, several critical system-level inconsistencies were identified.

These findings were not treated as isolated defects, but as indicators of deeper structural issues within the system.

---

### 1. Output Integrity Inconsistency

In multiple scenarios, the calculation results observed in the database did not match the results displayed in the UI.

Further investigation revealed that:

- The calculation formula used by the system was incorrect
- The system produced inconsistent outputs across different layers

This indicated a breakdown in output integrity, where the system could not guarantee that a single source of truth existed for calculation results.

**Impact:**
- High risk of incorrect billing
- Loss of trust in system-generated values
- Difficulty in validating correctness

---

### 2. Rule Composition Ambiguity

Complex scenarios involving Service Agreement (SA) types and addon configurations resulted in unclear tiering behavior.

Key challenges included:

- Lack of explicit rule hierarchy for tiering combinations
- Undefined interaction between multiple addon types
- Difficulty in predicting system behavior for combined rule conditions

This revealed that rule composition within the system was not clearly defined or consistently implemented.

**Impact:**
- Unpredictable calculation outcomes
- High dependency on implicit system behavior
- Increased risk of incorrect pricing logic

---

### 3. Uncontrolled Adjustment Mechanism

Adjustments could be applied at multiple stages of the process, including:

- Rating
- Billing
- Invoice

However, there was no clear boundary or governance regarding:

- Where adjustments should be applied
- Why they are applied at a specific stage
- How they affect downstream calculations

This created a condition where the same value could be altered multiple times across different layers without traceable justification.

**Impact:**
- Loss of calculation traceability
- Increased risk of data inconsistency
- Difficulty in auditing and explaining final billing values

---

### Overall Insight

These findings indicate that the primary issue was not isolated defects, but a lack of structural control in:

- Output consistency
- Rule definition
- Process boundaries

Without addressing these foundational issues, validating individual calculation results would lead to false confidence in system correctness.

## 7. Decision & Outcome

Given the identified system inconsistencies and unresolved ambiguity in calculation logic, the QA decision was to block validation for any flow that could not be clearly explained in terms of:

- Why the logic exists
- How the system is expected to execute it
- What business outcome it is intended to produce

The QA position was that unclear calculation behavior must not be treated as valid simply to maintain delivery speed.

Where clarification was not available but stakeholders still chose to proceed, QA explicitly stated that:

- The final outcome could not be guaranteed
- Validation status was incomplete
- Any resulting issue would fall under known and accepted risk, not confirmed system correctness

### Outcome

This approach established a clear quality boundary:

- Business-critical happy paths with sufficient clarity could continue to be validated
- Ambiguous or structurally inconsistent flows were blocked from receiving false approval
- Delivery pressure did not override the need for explainable and traceable calculation behavior

### Key Principle

If stakeholders want testing to happen earlier and more frequently, then business logic and system reasoning must also become earlier and clearer.

Without that clarity, accelerated testing only increases false validation and rework risk.

## 8. Evidence (NDA-Safe)

To support the findings and QA approach, evidence was structured in a way that demonstrates real system behavior without exposing sensitive data.

### QA Log Samples

Sample entries from QA Log were used to illustrate:

- Inconsistent validation results
- Mismatch between expected and actual behavior
- Repeated failure patterns across calculation stages

All data has been anonymized and simplified for demonstration purposes.

### Calculation Scenario Illustration

Simplified datasets were created to represent:

- Usage input (volume, energy, calorie)
- Expected vs actual calculation output
- Cases where system behavior deviated from expected logic

This demonstrates how inconsistencies can occur even with valid input.

### System Behavior Evidence

Examples include:

- UI showing successful processing while backend execution failed
- Service Agreement (SA) marked as not found despite being active
- Output discrepancies between database and UI

Screenshots and logs have been sanitized to remove sensitive identifiers.

### Control System Mapping

Each finding can be traced back to:

- QA Log (validation tracking)
- DEV Work logs (implementation changes)
- Calculation Control (input-output validation)
- Rhythm Control (iteration tracking)

This demonstrates how QA maintained visibility and control over system behavior.

---

### Important Note

All evidence presented in this case:

- Uses anonymized or simulated data
- Does not expose real customer or system identifiers
- Is intended to demonstrate QA approach and system understanding

The goal is not to replicate the exact production environment, but to illustrate how QA identifies, structures, and controls complex system issues.
