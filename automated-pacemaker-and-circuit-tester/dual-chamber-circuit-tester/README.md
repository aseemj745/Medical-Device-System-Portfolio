# Dual Chamber Circuit-Level Validation – Automated Test Flow

## Overview

This section documents the circuit-level validation flow implemented using the same automated test platform developed for pacemaker testing, extended to support full dual-channel electrical characterization and stress validation of dual chamber pacing circuits.

Circuit testing focuses on verifying electrical correctness, isolation, current integrity, and robustness of pacing circuits across both atrial and ventricular channels prior to final device assembly. The workflow is fully automated and designed for repeatability, safety, and production relevance.

---

## Test Philosophy

- Circuit validation follows the same automation framework as pacemaker testing
- Critical electrical tests act as gatekeepers for further testing
- **Continuous current monitoring is enforced across all test stages**
- **Any abnormal current condition results in immediate termination and routing to manual inspection**
- Both **bipolar and unipolar configurations are validated** across both channels wherever applicable
- All tests covering output or sensing are executed independently on the **A channel (atrial)** and **V channel (ventricular)**
- Results are fully automated with no manual intervention in measurement, evaluation, or logging

---

## Test Execution Strategy

### Stage 1 – Critical Gate Tests

The following tests are executed first and act as mandatory qualification checks:

1. **Amplitude & Leakage Test (UNIPOLAR + BIPOLAR — A & V Channel)**
   - Verifies output amplitude accuracy across both polarities for both channels
   - Detects unintended leakage between bipolar and unipolar configurations
   - Validates current consumption during output delivery
   
   **Failure (functional or current) results in immediate termination and manual inspection**

2. **Pulse Width Test (UNIPOLAR + BIPOLAR — A & V Channel)**
   - Verifies pulse width accuracy across both polarities for both channels
   - Monitors current consumption during pulse delivery
   
   **Failure (functional or current) results in immediate termination and manual inspection**

---

### Stage 2 – Electrical Characterization & Functional Tests

If all gate tests pass, the system executes a complete electrical validation sequence:

- **Sensitivity Test** (UNIPOLAR + BIPOLAR — A & V Channel)
- **Urgent Mode Test** (UNIPOLAR — A & V Channel)
- **Rate Test** (UNIPOLAR + BIPOLAR — A & V Channel)
- **Impedance Test** (UNIPOLAR + BIPOLAR — A & V Channel)
- **Battery Test** (BOL, ERI, EOL)
- **Noise Test** (UNIPOLAR + BIPOLAR — A & V Channel)
- **High Energy Stress Test** (UNIPOLAR + BIPOLAR — A & V Channel)
- **Trailing Edge & Slew Rate Test** (UNIPOLAR + BIPOLAR — A & V Channel)
- **Magnet Test** (UNIPOLAR + BIPOLAR — A & V Channel)

**Current consumption is continuously monitored during every test stage.**
Any out-of-tolerance current condition results in immediate termination and routing to manual inspection.

---

### Stage 3 – Dual Chamber Mandatory Tests

The following tests are always executed for all dual chamber circuits and are not model-dependent:

- **Rate Responsive Test** — Verifies rate-adaptive response in DDDR mode
- **AV Delay Test** — Verifies AV synchrony across pace delay, sense delay, and upper rate AV follow behavior

These tests are mandatory for all dual chamber circuits regardless of programmed model variant.

---

## Failure Handling & Re-Test Logic

- All **non-critical functional failures** are logged and highlighted in the test report
- After full test execution, the system evaluates overall results
- Individual failed tests can be re-executed once to rule out transient effects
- **Failures caused by current violations or gate test failures are not eligible for re-test and are directly routed to manual inspection**
- Persistent failures after re-test are routed to manual inspection

---

## Test Coverage

- Bipolar and unipolar output validation across both atrial and ventricular channels
- Full independent A & V channel characterization across all electrical parameters
- Full load simulation across all supported impedance conditions per channel
- Electrical stress testing under worst-case scenarios across both channels
- AV synchrony and inter-channel timing validation
- Continuous current integrity verification using external measurement instrumentation

---

## Regression Testing

- Successfully validated **300+ dual chamber pacing circuits** prior to deployment on the production testing floor

---

## Status

- Dual-chamber circuit validation: Implemented and actively used in Production QC
