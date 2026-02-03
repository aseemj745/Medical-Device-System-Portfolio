## Automated Circuit Test System – Hardware Architecture

This setup is used for automated testing and validation of pacemaker circuits. The architecture supports controlled power sourcing, current measurement, signal injection, and automated measurement under different operating conditions.

### Block Description and Interfacing

**PC (Python Test Framework)**  
The PC runs Python-based test scripts that coordinate power control, current measurement, signal injection, and data logging. All connected instruments and modules are accessed through custom wrappers or standard communication interfaces.

**Test Control PCB (Arduino + Relays + Load + Power Switching)**  
The Test Control PCB manages:
- Relay-based routing of signals and power
- Switching between different power sources
- Application of reference load to the circuit under test  
The onboard microcontroller controls all switching operations based on commands received from the PC.

**Programmable Digital Power Supply**  
The programmable PSU provides controlled power to the circuit during specific test conditions. Voltage and current limits are set by the PC through USB/Serial communication.

**Battery Source**  
A battery is used as an alternate power source to simulate real operating conditions. Switching between the battery and the programmable PSU is handled on the Test Control PCB using relays.

**Low-Current Measurement Module**  
This module is used to measure supply current during selected test steps. It is connected in the supply path of the circuit and is accessed by the PC through a USB/Serial interface using a custom Python wrapper.

**Function Generator**  
The function generator injects stimulus signals into the circuit when required. It is controlled by the PC and its output is routed through the Test Control PCB.

**Oscilloscope**  
The oscilloscope captures output signals from the circuit under test. Measurements are triggered and collected automatically via SCPI commands from the PC.

**Pacemaker Circuit (Device Under Test)**  
The circuit under test is powered through the Test Control PCB and remains connected to the reference load on board. Different operating modes and conditions are exercised through controlled power, signal injection, and measurement.

### System Intent

The circuit test system enables repeatable functional verification, current characterization, and power-mode testing by combining controlled power sourcing, automated measurement, and relay-based hardware switching.
