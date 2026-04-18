# Case 04 — Asynchronous Delay in Work Order Delivery

## 1. Context

The Work Order (WO) distribution process in MyTrace is expected to deliver tasks from Admin to Agents in a timely manner.

Timely delivery is critical because Agents rely on receiving tasks within operational time windows to perform actions such as customer calls or field visits.

---

## 2. Problem Description

During testing, it was observed that Work Orders did not always appear immediately after distribution.

Observed behaviors included:

- WO appearing with delay
- WO appearing only for some agents
- WO not appearing until manual refresh or re-trigger

This created uncertainty in whether the system had successfully processed the distribution.

---

## 3. Expected vs Actual Behavior

### Expected

- WO appears within a defined acceptable time window after distribution
- All assigned Agents receive the WO consistently
- Dashboard reflects the same state as Agent view

### Actual

- WO delivery timing was inconsistent
- Some Agents received WO earlier than others
- Dashboard and Agent views were not synchronized in time

---

## 4. Root Cause Hypothesis

The behavior suggested the system operates with asynchronous processing, potentially involving:

- Background jobs
- Message queues
- Event-driven updates

Potential failure points:

- Delayed job execution
- Queue backlog
- Event processing failure
- Inconsistent update propagation

---

## 5. QA Approach

QA focused on validating not only correctness, but also timing behavior.

Key validation activities included:

1. Measuring time between distribution and WO visibility
2. Comparing timing across:
   - Different Agents
   - Dashboard vs Agent view
3. Identifying patterns of delay or partial delivery
4. Observing whether manual actions (refresh/re-trigger) affected outcome

---

## 6. Validation Strategy

QA defined time-based validation boundaries:

- Immediate / Near real-time → acceptable
- Delayed but consistent → at risk
- Delayed and inconsistent → invalid

Without a defined SLA, QA treated timing inconsistency as a system risk.

---

## 7. Decision & Outcome

QA decision:

- WO delivery without consistent timing was classified as **at risk**
- Partial or delayed delivery beyond acceptable thresholds was treated as **invalid**

Where timing behavior could not be explained:

- Validation was limited
- Risk was explicitly documented

---

## 8. Key Insight

This case highlighted that:

> System correctness is not only about data accuracy, but also about delivery timing.

Even correct data becomes unusable if delivered too late for operational use.

---

## 9. Risk Statement

If the system operates with uncontrolled delay:

- Agents may miss execution windows
- Task prioritization becomes unreliable
- Operational efficiency is reduced

Risk ownership lies with:

- System owners (async processing design)
- Business stakeholders (operational expectations)
