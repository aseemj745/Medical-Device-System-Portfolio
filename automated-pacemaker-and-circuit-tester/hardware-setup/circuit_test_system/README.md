## Automated Circuit Test System – Hardware Architecture

This setup is used for automated testing and validation of pacemaker circuits. The architecture supports controlled power sourcing, current measurement, signal injection, and automated measurement under different operating conditions.

### Block Description and Interfacing

**PC (Python Test Framework)**  
The PC runs Python-based test scripts that coordinate power control, current measurement, signal injection, and data logging. All connected instruments and modules are accessed through custom wrappers or standard communication interfaces (USB, Serial, SCPI). The PC acts as the central controller for the entire test system, issuing commands and collecting measurement data.

---

**Test Control PCB (Arduino + Relays + Load + Power Switching)**  
The Test Control PCB is the central hardware interface layer and manages:
- Relay-based routing of signals and power
- Switching between different power sources
- Controlled connection of the circuit under test
- Integrated reference load for electrical testing  

The onboard microcontroller (ATmega328P) executes switching logic based on commands received from the PC.  
This board abstracts hardware complexity and enables flexible test sequencing using the same physical platform.

---

**Pacemaker Programmer (USB Interface)**  
The programmer is used to configure pacemaker parameters such as rate, pulse width, sensitivity, and mode. It is controlled from Python using a custom wrapper and communicates directly with the pacemaker during test execution.

---

**Power Supply & Current Measurement Module**  
This module provides controlled power to the device under test while simultaneously measuring supply current.  
It operates in the main supply path and is interfaced with the PC via USB.  

It is used for:
- Supplying stable test power
- Real-time current monitoring
- Detecting abnormal current conditions during validation

---

**Battery Source**  
A battery is used as an alternate power source to simulate real operating conditions and to eliminate noise introduced by USB-powered sources during sensitive measurements.

- Used specifically during **noise and sensing tests**
- Power source switching is handled on the Test Control PCB via relays

---

**Function Generator**  
The function generator injects stimulus signals (e.g., sensing signals, noise inputs) into the circuit when required.  
It is controlled by the PC, and its output is routed through the Test Control PCB.

---

**Oscilloscope**  
The oscilloscope captures output waveforms and electrical signals from the circuit under test.  
Measurement acquisition and triggering are automated using SCPI commands from the PC.

---

**Pacemaker Circuit (Device Under Test)**  
The circuit under test is powered through the Test Control PCB and remains connected to the onboard reference load.  
Different operating modes and conditions are exercised through controlled power delivery, signal injection, and automated measurement.

---

**Stepper Motor Jig (R-Mode Activity / Magnet Test)**  
A stepper motor-based jig provides controlled mechanical stimulation near the pacemaker for:
- Rate-responsive (R-mode) validation  
- Magnet response testing  

The motor is driven and synchronized through the Test Control PCB.

---

### System Intent

The circuit test system enables repeatable and production-relevant validation of pacemaker circuits by integrating:

- Controlled power sourcing with real-time current monitoring  
- Relay-based hardware abstraction and signal routing  
- Automated stimulus injection and waveform measurement  
- Dynamic power source switching (including battery isolation for low-noise testing)  

The system is designed to support both functional verification and deep electrical characterization under controlled and repeatable conditions.
