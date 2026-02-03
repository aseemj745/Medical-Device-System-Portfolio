# Test Hardware Overview

This folder documents the **custom test hardware** used in the automated pacemaker and circuit validation system.

The hardware was designed to support:
- Electrical stimulation and sensing
- Load and impedance simulation
- Channel configuration (single / dual)
- Automated, repeatable test execution

All images and descriptions are provided for **illustrative purposes only**.

---

## Hardware Architecture

The test setup consists of:

- Custom-designed PCBs for signal routing and load selection
- Relay-based switching for output configuration
- Embedded controller for deterministic hardware control
- Mechanical fixtures (jigs) for repeatable device interaction
- External laboratory instruments for measurement and verification

The same core hardware is reused across:
- Single-chamber pacemaker testing
- Dual-chamber pacemaker testing
- Pacing circuit validation

---

## Load and Configuration Control

The hardware supports multiple electrical configurations, including:

- Bipolar and unipolar output paths
- Programmable load simulation (e.g., 350Ω, 500Ω, 1000Ω, open, short)
- Independent channel selection for atrial and ventricular paths

Load switching and configuration are fully automated and controlled by embedded firmware.

---

## PCB Development and Iterations

Multiple PCB revisions were developed during system evolution:

- Initial revisions focused on functional validation
- Subsequent revisions corrected schematic import and layout issues
- Component selection was optimized for:
  - Manual solderability
  - Debug accessibility
  - Reliability during repeated testing

Design iterations were migrated from OrCAD to Altium Designer as part of system consolidation.

---

## Images in This Folder

The images included here show:
- PCB renders from different design iterations
- Assembled test boards
- Mechanical jigs and fixtures
- Overall testbench setup

No production identifiers, device markings, or confidential information are visible.

---

## Safety and Compliance Note

This hardware is intended for **engineering validation and test purposes only**.  
It is not a medical device and is not used directly on patients.
