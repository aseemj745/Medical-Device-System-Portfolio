## Automated Pacemaker Test System – Hardware Architecture

This setup is used for automated functional and system-level testing of single- and dual-chamber pacemakers. The architecture combines instrument automation, relay-based signal routing, onboard loading, device programming, and controlled mechanical activity.

### Block Description and Interfacing

**PC (Python Test Framework)**  
The PC runs the main test scripts written in Python. It controls all instruments, the test PCB, and the pacemaker programmer using USB/Serial and SCPI communication. Test sequencing, parameter changes, measurements, and result logging are handled here.

**Pacemaker Programmer (USB Interface)**  
The programmer is used to configure pacemaker parameters such as rate, pulse width, sensitivity, and mode. It is controlled from Python using a custom wrapper and communicates directly with the pacemaker during test execution.

**Test Control PCB (Arduino + Relays + Load)**  
This is the central hardware interface. It contains:
- An onboard microcontroller(ATmega328P) for relay control and motion coordination
- Relay-based routing for signal injection and measurement ans switching
- A reference electrical load on board that remains continuously connected to the pacemaker  
The PCB interfaces directly with the pacemaker, function generator, oscilloscope, and stepper motor jig.

**Function Generator**  
The function generator provides sensing or stimulus signals required during specific test cases. It is controlled by the PC via SCPI and its output is routed to the pacemaker through the Test Control PCB.

**Oscilloscope**  
The oscilloscope measures pacemaker output signals routed through the Test Control PCB. All waveform acquisition and measurements are automated via SCPI commands from the PC.

**Stepper Motor Jig (R-Mode Activity / Magnet Test)**  
A stepper motor-based jig provides controlled mechanical movement near the pacemaker for rate-responsive (R-mode) and magnet-related testing. The motor is driven and synchronized through the Test Control PCB.

**Pacemaker (Device Under Test)**  
The pacemaker is mounted on the jig and connected to the Test Control PCB. It remains continuously connected to the reference load throughout testing to maintain realistic operating conditions.

### System Intent

The system is designed to perform repeatable, automated pacemaker testing while maintaining continuous load connection, synchronized programming, and controlled measurement conditions.
