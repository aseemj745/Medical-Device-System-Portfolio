# Circuit-Level Validation – Automated Test Flow

## Overview
This section documents the circuit-level validation flow implemented using the same automated test platform developed for pacemaker testing, extended to support deeper electrical characterization and stress validation of pacing circuits.

Circuit testing focuses on verifying electrical correctness, isolation, current integrity, and robustness of pacing circuits prior to final device assembly. The workflow is fully automated and designed for repeatability, safety, and production relevance.

---

## Test Philosophy
- Circuit validation follows the same automation framework as pacemaker testing
- Critical electrical tests act as gatekeepers for further testing
- **Continuous current monitoring is enforced across all test stages**
- **Any abnormal current condition results in immediate termination and routing to manual inspection**
- Both **bipolar and unipolar configurations are validated**
- Results are fully automated with no manual intervention in measurement, evaluation, or logging

---

## Test Execution Strategy

### Stage 1 – Critical Gate Tests
The following tests are executed first and act as mandatory qualification checks:

1. **Amplitude & Leakage Test (Bipolar + Unipolar)**
   - Verifies output amplitude accuracy
   - Detects unintended leakage between bipolar and unipolar configurations
   - Validates current consumption during output delivery  
   **Failure (functional or current) results in immediate termination and manual inspection**

2. **Pulse Width Test (Bipolar + Unipolar)**
   - Verifies pulse width accuracy
   - Monitors current consumption during pulse delivery  
   **Failure (functional or current) results in immediate termination and manual inspection**

---

### Stage 2 – Electrical Characterization & Functional Tests
If all gate tests pass, the system executes a complete electrical validation sequence:

- Impedance testing (Bipolar + Unipolar)
- Sensitivity verification (Bipolar + Unipolar)
- Urgent mode validation (Unipolar)
- Rate verification (Bipolar + Unipolar)
- Battery monitoring (BOL, ERI ,EOL)
- Noise immunity testing (Bipolar + Unipolar)
- High-energy stress testing at maximum parameters
- Trailing edge and slew rate verification (Bipolar + Unipolar)
- Magnet response verification

**Current consumption is continuously monitored during every test stage.**  
Any out-of-tolerance current condition results in immediate termination and routing to manual inspection.

---

### Stage 3 – Model-Dependent Testing
For pacing circuits supporting **rate-responsive (R) mode**, an additional test is appended dynamically:

- Rate Responsive Rate Test

This behavior is automatically enabled based on circuit model identification.

---

## Failure Handling & Re-Test Logic
- All **non-critical functional failures** are logged and highlighted in the test report
- After full test execution, the system evaluates overall results
- Individual failed tests can be re-executed once to rule out transient effects
- **Failures caused by current violations or gate test failures are not eligible for re-test and are directly routed to manual inspection**
- Persistent failures are routed to manual inspection

---

## Test Coverage
- Bipolar and unipolar output validation across critical electrical parameters
- Full load simulation across all supported impedance conditions
- Electrical stress testing under worst-case scenarios
- Continuous current integrity verification using external measurement instrumentation

---

## Regression Testing 
- Successfully validated **500+ single chamber pacing circuits** prior to deployment on the production testing floor

---

## Status
- Single-chamber circuit validation: Implemented and actively used in Production QC
