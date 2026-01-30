# Automated Pacemaker and Circuit Test System

This repository documents the design and implementation of an automated test system developed for validation and production testing of implantable cardiac pacemakers and pacing circuits.

The system supports single-chamber and dual-chamber pacemakers, as well as detailed circuit-level validation, and is designed to replace manual bench testing with repeatable, instrument-driven workflows.

The focus of this project is:
- System-level validation
- Hardware–software integration
- Automated test execution
- Reliable pass/fail decision making in a production environment

## Scope of Testing
- Final pacemaker testing (single & dual chamber)
- Circuit-level validation under multiple electrical loads
- Automated signal acquisition and tolerance checking
- Battery and reliability testing
- Regression testing with re-test handling

## Repository Structure
- **Pacemaker Testing** – Functional validation of final pacemakers  
- **Circuit Testing** – Rigorous electrical validation of pacing circuits  
- **Hardware** – Test fixtures, PCB designs, and bench setup  

Each section contains its own README explaining test logic, flow, and hardware context.


