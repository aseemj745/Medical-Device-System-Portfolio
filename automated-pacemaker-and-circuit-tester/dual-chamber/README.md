# Dual-Chamber Pacemaker Test Flow

The dual-chamber test flow extends the single-chamber logic by validating both atrial (A) and ventricular (V) channels.

## Test Philosophy
- Identical automation strategy as single-chamber testing
- Channel-wise validation for atrial and ventricular paths
- Unified pass/fail decision at the end of the test cycle

## Test Sequence
1. OFF-mode verification
2. Parameter programming
3. Amplitude and leakage tests (A & V channels)
4. Sensitivity tests (A & V channels)
5. Rate and timing verification
6. Pulse-width verification
7. Impedance measurement
8. Noise test
9. Magnet response test
10. High-amplitude stress test
11. Final battery measurement
12. Power-off and result classification

## Failure Handling
- All tests complete before evaluation
- Failed tests can be re-executed once
- Persistent failures are routed to manual testing
