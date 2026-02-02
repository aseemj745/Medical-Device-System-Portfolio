# Circuit-Level Validation – Automated Test Flow

## Overview
This section documents the circuit-level validation flow implemented using the same automated test platform developed for pacemaker testing, extended to support deeper electrical characterization and stress validation of pacing circuits.

Circuit testing focuses on verifying electrical correctness, isolation, current integrity, and robustness of pacing circuits prior to final device assembly. The workflow is fully automated and designed for repeatability, safety, and production relevance.

---

## Test Philosophy
- Circuit validation follows the same automation framework as pacemaker testing
- Critical electrical tests act as gatekeepers for further testing
- Continuous current monitoring is enforced across all test stages
- Both bipolar and unipolar configurations are validated
- Results are logged automatically with clear PASS / FAIL classification

---

## Test Execution Strategy

### Stage 1 – Critical Gate Tests
The following tests are executed first and act as mandatory qualification checks:

1. **Amplitude & Leakage Test**
   - Verifies output amplitude accuracy
   - Detects unintended leakage between bipolar and unipolar configurations
   - Validates current consumption during output delivery  
   **Failure at this stage results in immediate termination and manual inspection**

2. **Pulse Width Test**
   - Verifies pulse width accuracy
   - Monitors current consumption during pulse delivery  
   **Failure at this stage results in immediate termination**

---

### Stage 2 – Electrical Characterization & Functional Tests
If all gate tests pass, the system executes a complete electrical validation sequence:

- Impedance testing under all defined load scenarios
- Sensitivity verification
- Urgent mode validation
- Rate verification
- Battery behavior monitoring
- Noise immunity testing
- High-energy stress testing at maximum parameters
- Trailing edge and slew rate verification
- Magnet response verification

Current consumption is continuously monitored during every test.  
Any out-of-tolerance current condition results in immediate termination.

---

### Stage 3 – Model-Dependent Testing
For pacing circuits supporting **rate-responsive (R) mode**, an additional test is appended dynamically:

- Rate Responsive Rate Test

This behavior is automatically enabled based on circuit model identification.

---

## Failure Handling & Re-Test Logic
- All non-critical test failures are logged and highlighted in the test report
- After full test execution, the system evaluates overall results
- Individual failed tests can be re-executed once to rule out transient effects
- Persistent failures are routed to manual inspection
- Final device status is reported as PASS or FAIL

---

## Test Coverage
- Bipolar and unipolar output validation
- Full load simulation across all supported impedances
- Electrical stress testing under worst-case conditions
- Current integrity verification using external measurement instrumentation

---

## Regression Testing 
- Successfully tested 500+ single chamber pacemaker circuit before deployment to the production testing floor.

---

## Status
- Single-chamber circuit validation: **Implemented and is actively used in Production QC**
- Dual-chamber circuit tester: **Under development**
