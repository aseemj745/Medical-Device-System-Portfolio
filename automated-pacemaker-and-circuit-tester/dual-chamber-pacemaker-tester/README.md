# Dual-Chamber Pacemaker Test Flow

This flow validates dual-chamber pacemakers using a fully automated test system with synchronized atrial (A) and ventricular (V) channel verification.

---

## Test Philosophy

- Uses the same automation framework as single-chamber testing  
- All electrical tests are executed on **both atrial and ventricular channels**  
- Critical conditions (reset state, battery, amplitude) are handled as **early gate checks**  
- Remaining tests are executed sequentially with final evaluation  
- Only the **final validated result** is retained in logs  

---

## Stage-Based Initialization Logic

- **Stage 1 & 2**
  - Device must be in OFF mode  
  - If not in OFF mode → treated as reset  
  - **Immediately routed to manual inspection (no further testing)**  

- **Stage 3 & 4**
  - Device is expected to retain programmed parameters  
  - If parameters are invalid → treated as reset  
  - **Immediately routed to manual inspection**  

---

## Test Sequence

1. OFF-mode / parameter validation (stage-dependent)  
2. Set nominal test parameters  
3. **Initial battery test (mandatory pre-check)**  

4. **Amplitude & leakage test (A & V channels)**  
   - Critical gate condition  
   - Failure → **immediate exit to manual inspection**  

5. Sensitivity test (A & V channels)  
6. Rate & timing verification (A & V channels)  
7. Pulse-width verification (A & V channels)  
8. Impedance measurement (A & V channels)  
9. Noise test (A & V channels)  
10. Magnet response test  
11. Trailing edge & slew rate verification (A & V channels)  
12. Rate-responsive (R-mode) test 
13. AV delay test
14. Final battery measurement  

15. Final evaluation and classification  

---

## Failure Handling

- Initial battery test failure → **manual inspection**  
- Amplitude test failure → **immediate cut-off to manual inspection**  

- Other test failures:
  - Logged during execution  
  - Evaluated at end of test cycle  
  - One re-test allowed for failed tests only  

- Re-test behavior:
  - Pass → **previous failed value is overwritten (final PASS)**  
  - Fail → **device marked FAIL and routed to manual inspection**  

---

## Data Logging

- All results are automatically logged to structured Excel reports  
- Failed parameters are highlighted  
- Only the **final outcome per parameter is retained**  
- Final PASS / FAIL decision is recorded per device  

---

## Regression Testing

- Successfully tested **1200+ dual-chamber pacemakers** before deployment to production testing  

---

## Status

- Dual-chamber pacemaker validation: **Implemented and actively used in Production QC**
