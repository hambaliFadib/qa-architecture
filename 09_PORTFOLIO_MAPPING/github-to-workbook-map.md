# GitHub to Workbook Mapping

This document defines how QA Architecture cases are mapped to real execution artifacts in the QA Delivery Control system.

---

## Mapping Overview

| Case | Focus Area | Workbook Source |
|------|-----------|----------------|
| Case 01 — Multi-role Flow | State Consistency | QA_LOG, DEV_WORK, RHYTHM_CONTROL |
| Case 02 — Calculation | Logic Validation | QA_LOG_RBI, CALC_CONTROL |
| Case 03 — Integration Failure | Data Delivery | QA_LOG, DEV_WORK_DB |
| Case 04 — Async Delay | Timing | RHYTHM_CONTROL |
| Case 05 — Data Contract | Data Integrity | QA_LOG, CALC_CONTROL |

---

## QA Log Mapping

QA Log acts as the central tracking system.

Each entry should include:

- Related Case ID (e.g., CASE-02)
- Module / Flow (e.g., Calculation, WO Flow)
- Issue Type:
  - State
  - Logic
  - Integration
  - Timing
  - Data
- Validation Status:
  - Valid
  - At Risk
  - Invalid

This allows direct traceability from real defects to architectural cases.

---

## Calculation Control Mapping

Used primarily for Case 02.

Tracks:

- Input data
- Expected output
- Actual output
- Validation result

Ensures calculation correctness is verifiable and repeatable.

---

## DEV Work Mapping

Tracks implementation progress across:

- FE
- BE
- DB

Used to:

- Link QA findings to development changes
- Monitor resolution of issues
- Identify impact of system updates

---

## Rhythm Control Mapping

Tracks:

- Iteration cycles
- Repeated failures
- Regression patterns

Used to:

- Identify instability trends
- Support timing-related validation (Case 04)

---

## Objective

The purpose of this mapping is to ensure that:

- QA architecture is not theoretical
- All findings are traceable to real execution
- Decisions are backed by structured evidence
