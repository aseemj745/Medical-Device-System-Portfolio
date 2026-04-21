# Single-Chamber Pacemaker Automated Test Flow

This flow validates final single-chamber pacemakers in a fully automated manner across multiple production stages.

---

## Test Philosophy

- Test execution is **stage-aware (Stage 1–4)** and controlled via command-line inputs  
- Device state is validated before test execution (OFF mode / parameter integrity)  
- A **pre-test initialization step** ensures consistent starting conditions  
- Critical failures trigger **immediate routing to manual inspection**  
- Non-critical failures are **logged and evaluated after full test execution**  
- A single re-test is allowed for failed parameters to eliminate transient errors  

---

## Pre-Test Validation

Before starting electrical testing:

1. **Stage-Based Reset Logic**
   - **Stage 1 & 2**:  
     - Device must be in OFF mode  
     - If not, it is reset  
   - **Stage 3 & 4**:  
     - Existing programmed parameters are verified  
     - If valid → continue without reset  
     - If invalid → device is reset  

2. **Reset State Handling**
   - If the device is detected to be already in a reset state,  
     → it is **immediately removed from testing and sent for manual inspection**  

3. **Nominal Parameter Setup**
   - Device is programmed with predefined nominal parameters  

4. **Initial Battery Test**
   - Battery is verified **before any electrical test begins**  
   - Failure results in **immediate routing to manual inspection**  

---

## Test Sequence

After successful pre-validation, the following tests are executed:

1. Amplitude and leakage verification *(critical gate test)*  
2. Sensitivity test  
3. Rate verification  
4. Pulse-width verification  
5. Impedance measurement using predefined reference load  
6. Noise test  
7. Magnet response test  
8. Trailing edge, slew rate, and high-amplitude validation  
9. **Rate-responsive test (only if device supports R-mode)**  
10. Final battery measurement  

---

## Failure Handling

- **Amplitude Test Failure**  
  - Considered a **hard failure**  
  - Device is immediately routed to manual inspection  
  - No further tests are executed  

- **Other Test Failures**  
  - Failures are logged during execution  
  - Test flow continues without interruption  

- **Post-Test Evaluation**
  - If any test fails:
    - Only failed tests are re-executed once  
    - If re-test passes → device may PASS  
    - If re-test fails → device is routed to manual inspection  

---

## Data Logging

- All test results are automatically logged to structured Excel reports  
- Failed parameters are clearly highlighted  
- In case of re-test:
  - Only the **final result is retained**
  - If the re-test passes → previous failed value is overwritten  
  - If the re-test fails → final result remains FAIL  
- Final PASS / FAIL decision is recorded per device  

---

## Regression Testing 

- Successfully tested **2000+ single-chamber pacemakers** prior to deployment on the production testing floor  

---

## Status

- Single-chamber pacemaker validation: **Implemented and actively used in Production QC**
