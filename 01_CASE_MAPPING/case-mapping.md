# QA Case to Execution Mapping

This document defines how each QA Architecture case is connected to real execution artifacts within the QA Delivery Control System.

The purpose of this mapping is to demonstrate that all architectural thinking is grounded in actual QA operations.

---

## Mapping Overview

| Case ID | Case Title | Focus Area |
|--------|-----------|------------|
| CASE-01 | Multi-role Flow Consistency | State & Data Consistency |
| CASE-02 | Calculation Validation | Business Logic Integrity |
| CASE-03 | Integration Failure | Data Delivery Integrity |
| CASE-04 | Async Delay | Timing & Event Consistency |
| CASE-05 | Data Contract Conflict | Data Structure & Source of Truth |

---

## CASE-01 — Multi-role Flow Consistency

**Focus:**
Ensuring consistency of state and data across Admin and Agent roles.

**Workbook Mapping:**
- QA_LOG → tracks mismatch issues (status, dashboard vs DB)
- DEV_WORK_FE/BE → tracks implementation changes affecting state
- RHYTHM_CONTROL → tracks repeated inconsistency and regression

**Validation Strategy:**
- Compare Admin vs Agent vs Database state
- Identify mismatch patterns

**Evidence Type:**
- Dashboard vs DB mismatch sample
- Status inconsistency example

---

## CASE-02 — Calculation Validation

**Focus:**
Ensuring correctness of business calculation logic.

**Workbook Mapping:**
- QA_LOG_RBI → tracks calculation-related defects
- CALCULATION_CONTROL → validates input vs expected vs actual output

**Validation Strategy:**
- Verify formula correctness
- Validate output consistency across layers

**Evidence Type:**
- Calculation scenario sample
- Expected vs actual output comparison

---

## CASE-03 — Integration Failure

**Focus:**
Ensuring complete data delivery in Work Order integration.

**Workbook Mapping:**
- QA_LOG → tracks missing data issues
- DEV_WORK_DB → tracks data mapping / query fixes

**Validation Strategy:**
- Verify completeness of customer & product data
- Identify source vs integration issue

**Evidence Type:**
- Partial data WO example
- Data injection scenario (sanitized)

---

## CASE-04 — Async Delay

**Focus:**
Ensuring timing consistency in Work Order delivery.

**Workbook Mapping:**
- RHYTHM_CONTROL → tracks delay patterns
- QA_CHECKPOINT_LOG → tracks timing observation

**Validation Strategy:**
- Measure delay between action and visibility
- Compare across roles

**Evidence Type:**
- Delay timeline example
- Partial delivery case

---

## CASE-05 — Data Contract Conflict

**Focus:**
Ensuring data structure consistency across system layers.

**Workbook Mapping:**
- QA_LOG → tracks data inconsistency
- CALCULATION_CONTROL → validates structured data input

**Validation Strategy:**
- Compare DB vs UI data structure
- Identify missing / invalid fields

**Evidence Type:**
- Missing field example
- Data mismatch scenario

---

## Overall Objective

This mapping ensures that:

- QA cases are not theoretical
- Every finding is traceable to real execution
- All validation decisions are supported by structured artifacts

The system demonstrates how QA operates as a control layer, connecting business intent, system behavior, and validation outcomes.
