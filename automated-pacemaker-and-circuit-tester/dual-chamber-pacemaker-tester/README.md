# Dual-Chamber Pacemaker Automated Test Flow

This flow validates dual-chamber pacemakers using a fully automated test system with synchronized atrial (A) and ventricular (V) channel verification.

---

## Test Philosophy

- Uses the same automation framework as single-chamber testing  
- All electrical tests are executed on **both atrial and ventricular channels**  
- Critical conditions (reset state, battery, amplitude) are handled as **early gate checks**  
- Remaining tests are executed sequentially with final evaluation  
- Test execution is controlled via **command-line arguments (stage selection and re-test control)**  
- Only the **final validated result** is retained in logs  

---

## Stage-Based Initialization Logic

- **Stage 1 & 2**
  - Device must be in OFF mode  
  - If not in OFF mode → device is reset  
  - If already found in reset state → **immediate manual inspection (no further testing)**  

- **Stage 3 & 4**
  - Device is expected to retain programmed parameters  
  - If parameters are invalid → device is reset  
  - If already found in reset state → **immediate manual inspection**  

---

## Test Sequence

1. OFF-mode / parameter validation (stage-dependent)  
2. Set nominal test parameters  
3. **Initial battery test (mandatory pre-check)**  

4. **Amplitude & leakage test (A & V channels)**  
   - Critical gate condition  
   - Failure → **immediate exit to manual inspection (power OFF)**  

5. Sensitivity test (A & V channels)  
6. Rate test  
7. Pulse-width test (A & V channels)  
8. Impedance test (A & V channels)  
9. Noise test (A & V channels)  
10. Magnet response test (A & V channels)  
11. Trailing edge & slew rate test (A & V channels)  
12. Rate-responsive (R-mode) test  
13. AV delay test 
14. Final battery measurement  

15. Final evaluation and classification  

---

## Failure Handling

- Initial battery test failure → **power OFF and manual inspection**  
- Amplitude test failure → **immediate cut-off and manual inspection**  

- Other test failures:
  - Logged during execution  
  - Evaluated at the end of the full test cycle  
  - Re-test allowed for **failed tests only**  

- Re-test behavior:
  - Pass → **previous failed value is overwritten (final PASS)**  
  - Fail → **device marked FAIL and routed to manual inspection**  

- Devices detected in **reset state during initialization**:
  - **Immediately removed from test flow**
  - Routed directly to manual inspection (no further actions)

---

## Data Logging

- All results are automatically logged to structured Excel reports  
- Failed parameters are highlighted  
- Only the **final outcome per parameter is retained** (re-test overwrites previous result)  
- Final PASS / FAIL decision is recorded per device  

---

## Regression Testing

- Successfully tested **1200+ dual-chamber pacemakers** before deployment to production testing  

---

## Status

- Dual-chamber pacemaker validation: **Implemented and actively used in Production QC**
