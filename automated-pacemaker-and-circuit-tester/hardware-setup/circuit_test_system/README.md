## Automated Circuit Test System – Hardware Architecture

This setup is used for automated testing and validation of pacemaker circuits. The architecture supports controlled power sourcing, current measurement, signal injection, and automated measurement under different operating conditions.

---

## System Overview

The test system combines embedded hardware, instrumentation, and Python-based automation to enable repeatable and production-relevant validation of pacing circuits.

It supports:
- Automated electrical parameter verification
- Real-time current monitoring
- Multi-mode test execution
- Configurable test sequencing
- Production-grade logging and validation workflows

---

## Hardware Setup (Actual Implementation)

![Full Test Setup](./assets/full_setup.png)

The above image shows the complete testbench setup, including:

- Test Control PCB with relay-based switching
- Pacemaker programmer interface
- Power & current measurement module
- Function generator for stimulus injection
- Oscilloscope for waveform capture
- Stepper motor jig for R-mode and magnet testing
- Device under test (DUT) mounted on test fixture

This setup reflects the actual production validation environment used for circuit-level testing.

---

## Block Description and Interfacing

**PC (Python Test Framework)**  
The PC runs Python-based test scripts that coordinate power control, current measurement, signal injection, and data logging. All connected instruments and modules are accessed through custom wrappers or standard communication interfaces (USB, Serial, SCPI). The PC acts as the central controller for the entire test system.

---

**Test Control PCB (Arduino + Relays + Load + Power Switching)**  
The Test Control PCB is the central hardware interface layer and manages:
- Relay-based routing of signals and power
- Switching between power sources
- Controlled connection of DUT
- Integrated reference load for electrical validation  

The onboard microcontroller (ATmega328P) executes switching logic based on commands received from the PC.

---

**Pacemaker Programmer (USB Interface)**  
Used to configure pacemaker parameters such as rate, pulse width, sensitivity, and operating mode. Controlled via Python using a custom communication wrapper.

---

**Power Supply & Current Measurement Module**  
Provides regulated power to the DUT while simultaneously measuring supply current.

Used for:
- Stable power delivery
- Continuous current monitoring
- Detection of abnormal current conditions during testing

---

**Battery Source**  
Used as an alternate power source during **noise and sensing tests** to eliminate noise introduced by USB-powered sources.

Power source selection is handled dynamically via relays on the Test Control PCB.

---

**Function Generator**  
Injects stimulus signals (noise/sensing inputs) into the DUT. Controlled via the PC and routed through the Test Control PCB.

---

**Oscilloscope**  
Captures output waveforms and electrical characteristics of the DUT. Controlled via SCPI commands for automated acquisition.

---

**Pacemaker Circuit (Device Under Test)**  
The DUT is powered through the Test Control PCB and remains connected to the onboard reference load. All test conditions are applied via controlled switching and automation.

---

**Stepper Motor Jig (R-Mode / Magnet Testing)**  
Provides controlled mechanical interaction for:
- Rate-responsive validation
- Magnet mode testing  

Controlled and synchronized through the Test Control PCB.

---

## Software Interface & Execution

![Console Interface](./assets/console_output.png)

The test system is operated through a Python-based CLI interface.

Key features:
- Modular test execution using argument-based commands
- Support for running individual or grouped test cases
- Parameterized testing (e.g., sensitivity values, polarity selection)
- Dual tester support (T1 / T2)
- Clear mapping between test arguments and validation steps

Examples:
- Run full test suite  
- Execute selected tests  
- Run parameter-specific validations  
- Perform polarity-specific or mixed test conditions  

This interface enables flexible and controlled execution of validation workflows.

---

## System Behavior

The system performs:

- Automated test sequencing
- Real-time evaluation of electrical parameters
- Continuous current monitoring across all stages
- Immediate termination on critical failures
- Structured logging with PASS/FAIL classification
- Optional re-test logic for non-critical failures

---

## System Intent

The circuit test system enables repeatable and production-relevant validation of pacemaker circuits by integrating:

- Controlled power sourcing with real-time current monitoring  
- Relay-based hardware abstraction and signal routing  
- Automated stimulus injection and waveform measurement  
- Dynamic power source switching (including battery isolation for low-noise testing)  

The system is designed to support both functional verification and deep electrical characterization under controlled and repeatable conditions.
