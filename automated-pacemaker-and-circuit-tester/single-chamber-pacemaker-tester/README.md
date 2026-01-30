# Single-Chamber Pacemaker Test Flow

This flow validates final single-chamber pacemakers in a fully automated manner.

## Test Philosophy
- All tests run sequentially in a single pass
- No interruption during execution
- Failures are evaluated only after completion of the full test
- A single re-test is allowed for failed tests to rule out transient effects

## Test Sequence
1. OFF-mode verification (reset check)
2. Parameter programming
3. Amplitude and leakage verification
4. Sensitivity test using CENELEC signal
5. Rate verification
6. Pulse-width verification
7. Impedance measurement (500 Ω load)
8. Noise test
9. Magnet response test
10. High-amplitude stress test
11. Final battery measurement
12. Power-off and result classification

## Failure Handling
- If any test fails, the specific test can be re-executed once
- If the re-test passes, the result is updated and the device can PASS
- If the re-test fails, the device is routed to manual testing

##Status
Single-chamber pacemaker validation: Implemented and is actively used in Production QC
