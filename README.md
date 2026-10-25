# Portable Pocket Oscilloscope & Logic Analyzer

A compact, hardware-isolated digital oscilloscope and logic analyzer built around the Raspberry Pi Pico 2 (RP2350) microcontroller. This project focuses on high-speed ADC sampling, hardware-level circuit protection, and signal conditioning frontend design.

## System Architecture Overview

The system captures analog and digital signals, conditions them through an analog frontend to match the safe input voltage range of the RP2350, and streams the processed data over USB to a host PC using PulseView.

---

## Hardware Engineering

### 1. Circuit Design & PCB Routing (`/hardware`)
Designed and routed a custom single-board layout using **KiCad**, prioritizing signal isolation and noise reduction.
* **Analog Frontend (AFE):** Implemented an input impedance matching network (1 MΩ standard) paired with an operational amplifier configuration for signal attenuation and shifting, allowing safe sampling of signals beyond the microcontroller's native 3.3V limit.
* **Overvoltage & Transient Protection:** Integrated clamping diodes to protect the RP2350 GPIO and ADC pins from accidental overvoltage spikes.
* **USB Port Isolation:** Implemented galvanic isolation on the USB data and power lines to decouple the circuit from the host PC's ground loop, mitigating switching noise and protecting test equipment.

---

## Firmware & Software Architecture (`/firmware`)

The main software is based on the work of [sigrok-pico](https://github.com/pico-coder/sigrok-pico) with only minor changes in the firmware to output the read value after voltage attenuation. 

---

## Repository Directory Structure

```text
├── 3d_models/                # FreeCAD project files for the case, and step model of the PCB
├── docs/                     # Schematics (PDF/PNG), layout captures, and component datasheets
├── hardware/                 # KiCad project files (Schematics, PCB layout, footprints)
└── firmware/                 # Microcontroller source code (C/C++) and build files
```

---

## Contributors & Credits
* **Alexandre Dionne** – Solo Hardware conception, analog frontend topology design, and firmware modification.
* [**sigrok-pico project team**](https://github.com/pico-coder/sigrok-pico) for the main firmware.
