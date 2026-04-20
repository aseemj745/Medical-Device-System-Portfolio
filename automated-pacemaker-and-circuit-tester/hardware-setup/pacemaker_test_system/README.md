## Automated Pacemaker Test System – Hardware Architecture

This setup is used for automated functional and system-level testing of single- and dual-chamber pacemakers. The architecture integrates instrument automation, relay-based signal routing, device programming, and controlled mechanical stimulation to enable repeatable and production-relevant validation.

---

## System Overview

The test system combines embedded hardware, instrumentation, and Python-based automation to perform:

- Automated functional validation of pacemaker operation  
- Parameter verification across multiple operating modes  
- Continuous electrical loading under realistic conditions  
- Controlled mechanical stimulation for R-mode and magnet testing  
- Structured and repeatable test execution across production stages  

---

## Hardware Setup (Actual Implementation)

The setup consists of:

- Test Control PCB with relay-based switching and onboard load  
- Pacemaker programmer interface  
- Function generator for stimulus injection  
- Oscilloscope for waveform capture  
- Stepper motor jig for R-mode and magnet testing  
- Device under test (mounted on mechanical fixture)  

The arrangement reflects an actual validation environment used for staged testing during manufacturing and verification.

---

## Block Description and Interfacing

**PC (Python Test Framework)**  
The PC runs Python-based test scripts that coordinate all system components. It controls the test PCB, pacemaker programmer, and instruments using USB/Serial and SCPI communication.  
Test sequencing, parameter configuration, measurement acquisition, and logging are fully automated at this layer.

---

**Pacemaker Programmer (USB Interface)**  
The programmer configures device parameters such as rate, pulse width, sensitivity, and operating mode.  
It is controlled via Python using a custom wrapper and communicates directly with the pacemaker during test execution.

---

**Test Control PCB (Arduino + Relays + Load)**  
This is the central hardware interface layer and manages:

- Relay-based routing of signals and measurement paths  
- Controlled connection between instruments and the pacemaker  
- Continuous connection of onboard reference load  
- Coordination of external components such as the stepper motor jig  

The onboard microcontroller (ATmega328P) executes switching logic and synchronization based on commands from the PC.

---

**Function Generator**  
Provides sensing and stimulus signals required during specific validation scenarios.  
It is controlled via SCPI from the PC, and its output is routed through the Test Control PCB.

---

**Oscilloscope**  
Captures pacemaker output waveforms and electrical characteristics.  
Measurement triggering, acquisition, and parameter extraction are fully automated via SCPI commands.

---

**Stepper Motor Jig (R-Mode Activity / Magnet Test)**  
A stepper motor-based single-axis jig provides controlled mechanical interaction with the pacemaker for:

- Rate-responsive (R-mode) validation  
- Magnet response testing  

The jig is driven and synchronized through the Test Control PCB, ensuring repeatable motion profiles during testing.

---

**Pacemaker (Device Under Test)**  
The pacemaker is mounted on the jig and connected to the Test Control PCB.  
It remains continuously connected to the onboard reference load to maintain realistic operating conditions throughout testing.

---

## Software Interface & Execution

The system is operated via a Python-based command-line interface (CLI) that enables:

- Modular test execution using argument-based commands  
- Stage-wise validation aligned with production flow  
- Support for single- and dual-chamber configurations  
- Parameterized testing (e.g., sensitivity, rate, polarity conditions)  
- Execution of full test suites or selected test subsets  
- Re-testing of failed parameters  

The CLI structure reflects real production usage, where tests are executed across multiple stages such as:

- Post-assembly validation  
- Post-welding and leak testing  
- Pre burn-in verification  
- Post burn-in validation  

---

## System Behavior

The system performs:

- Automated test sequencing across defined stages  
- Continuous electrical loading during all tests  
- Real-time waveform acquisition and validation  
- Synchronization between programming, measurement, and stimulation  
- Structured PASS/FAIL evaluation for each test step  

---

## System Intent

The pacemaker test system enables controlled and repeatable validation by integrating:

- Automated device programming and parameter control  
- Relay-based hardware abstraction and signal routing  
- Continuous reference loading for realistic operation  
- Automated waveform measurement and analysis  
- Controlled mechanical stimulation for R-mode and magnet testing  

The system is designed to ensure reliable functional verification across different production stages while maintaining consistency, traceability, and test repeatability.
