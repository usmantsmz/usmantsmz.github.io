---
title: "R&D Embedded System: Developing Bluetooth BLE Tracking Device using TI CC2650"
date: 2026-03-04
permalink: /blog/ble-tracking-device-ti-cc2650/
tags:
  - Embedded Systems
  - IoT
  - Bluetooth Low Energy
  - Texas Instruments
  - CC2650
  - Firmware Development
  - RnD
excerpt: "Research and development of a custom Bluetooth Low Energy (BLE) tracking device based on TI CC2650. Covering hardware design, firmware architecture, power optimization, and real-world implementation."
---

R&D Embedded System: Developing Bluetooth BLE Tracking Device using TI CC2650
======
Introduction
------

As part of my research and development initiative in Embedded Systems and IoT devices, I designed and developed a custom Bluetooth Low Energy (BLE) tracking device based on the Texas Instruments CC2650 microcontroller.

This project focused on:
- Low power wireless communication
- Custom PCB hardware design
- Firmware development using TI RTOS
- BLE beacon & tracking implementation
- Industrial-ready embedded architecture
- This article documents the complete engineering approach behind the system.

Why TI CC2650?
------

The TI CC2650 was selected due to:
- Ultra-low power ARM Cortex-M3 architecture
- Integrated BLE stack
- TI-RTOS support
- Industrial-grade RF performance
- Secure and scalable firmware architecture

This SoC is ideal for long battery-life IoT tracking devices.

Hardware Architecture
------
1️⃣ Development Phase – LaunchPad
------
Initial prototyping was performed using:
- TI CC2650 LaunchPad
- Code Composer Studio (CCS)
- BLE Stack v2.x
- TI-RTOS
This stage validated:
- BLE advertising performance
- Power consumption profile
- UART debugging interface
- GPIO & peripheral configuration

2️⃣ Custom PCB Design

After validation, I designed a custom BLE tracking board including:
- CC2650 MCU
- Onboard antenna matching circuit
- USB power interface
- Buzzer output
- Button input
- Status LED
- External sensor header
Design considerations:
- RF trace impedance matching
- Proper grounding for BLE stability
- Low-noise power regulation
- Compact form factor

Firmware Architecture
------
The firmware was structured using TI-RTOS task-based architecture:
Main Components:
- BLE Advertising Task
- Event Handler Task
- Power Management Task
- Peripheral Control Task
- OTA Ready Structure

BLE Implementation

The device operates as:
- BLE Broadcaster
- Custom GATT profile
- Unique Device ID
- Configurable advertising interval

Possible use cases:
- Asset tracking
- Warehouse monitoring
- Equipment tracking
- Personnel badge tracking
- Industrial IoT gateway integration

Power Optimization Strategy
------
Since BLE tracking devices must be low-power, optimization included:
- Deep sleep mode usage
- Reduced advertising interval tuning
- Peripheral shutdown management
- Clock source optimization
- Low leakage PCB layout

Result:

✔ Stable BLE broadcast
✔ Optimized battery consumption
✔ Industrial-ready performance

Engineering Challenges
------
Some technical challenges encountered:
- RF noise during initial PCB revision
- BLE stack memory optimization
- Task priority balancing in TI-RTOS
- Power spikes during active advertising
- All resolved through iterative R&D and firmware refinement.

Industrial & IoT Applications
------
This BLE tracking device can be integrated into:
- Smart factory systems
- Asset management platforms
- Cold storage monitoring
- Industrial automation networks
- Gateway-based IoT systems

Tools & Technologies Used
------
- Embedded C
- TI-RTOS
- Code Composer Studio
- BLE Stack
- PCB Design (Altium / equivalent)
- Oscilloscope & RF testing tools

Future Development
------
Planned improvements:
- Secure BLE pairing
- Mobile app integration
- Cloud dashboard integration
- Gateway MQTT bridge
- Battery health monitoring

Conclusion
------
This project demonstrates my hands-on experience in:
- Embedded firmware engineering
- BLE communication systems
- Custom hardware development
- Industrial IoT device architecture
- End-to-end R&D lifecycle

If you are looking for an engineer experienced in low-power IoT systems and embedded R&D, feel free to connect with me.
