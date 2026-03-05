---
title: "How to Read Temperature and Humidity Sensor AGH3485 Using Modbus Poll"
date: 2026-03-05
slug: read-agh3485-modbus-poll-rs485-temperature-humidity
categories:
  - industrial-iot
tags:
  - modbus
  - rs485
  - industrial-sensor
  - humidity-sensor
  - temperature-sensor
  - modbus-poll
  - agh3485
---
![How to Read Temperature and Humidity Sensor AGH3485 Using Modbus Poll](/images/usmantsmz-asair-sensor-agh3485.jpg)
Industrial sensors commonly use **RS485 Modbus RTU communication** because of its reliability and simplicity in industrial environments. One of the commonly used devices is the **ASAIR AGH3485 temperature and humidity transmitter**.

In this tutorial, I will explain step-by-step how to:

- Read temperature and humidity data
- Identify the baud rate used by the sensor
- Change the Modbus Slave ID
- Change the baud rate

using the popular industrial testing software **Modbus Poll**.

This tutorial is useful for **IoT engineers, automation engineers, and embedded developers** working with **RS485 industrial sensors**.

---

# Sensor Overview

The **AGH3485** is a digital temperature and humidity transmitter that communicates using **Modbus RTU over RS485**.

Typical applications include:

- Environmental monitoring
- Industrial automation
- Smart agriculture
- Data logging systems
- IoT weather stations

Main features:

| Parameter | Value |
|--------|--------|
Temperature range | -40°C to 60°C |
Humidity range | 0 – 99.9% RH |
Protocol | Modbus RTU |
Interface | RS485 |
Default Baudrate | 9600 |
Default Slave ID | 1 |

---

# Hardware Connection

The sensor uses a **4-wire connection**:

| Wire Color | Function |
|-----------|-----------|
Red | Power +12V to +32V |
Black | Ground |
Yellow | RS485 A+ |
White | RS485 B- |

Typical connection:

Make sure:

- A → A
- B → B
- Ground connected

---

# Software Required

Download and install:

**Modbus Poll**

This is one of the most widely used tools for testing **Modbus RTU devices**.

It allows engineers to:

- Read holding registers
- Write configuration registers
- Debug RS485 communication

---

# Default Modbus Settings

Factory default configuration:
Slave ID : 1
Baudrate : 9600
Data bits : 8
Parity : None
Stop bit : 1
Protocol : Modbus RTU

---

# Step 1 — Connect Using Modbus Poll

Open:
Connection → Connect

Configure:
Port : COMx
Baudrate : 9600
Data bits : 8
Parity : None
Stop bits : 1
Mode : RTU


Click **OK**.

If the configuration is correct, the device will respond to Modbus queries.

---

# Step 2 — Reading Temperature and Humidity Data

Open:
Setup → Read/Write Definition

Configuration:
Slave ID : 1
Function : 03 Holding Registers
Address : 0
Quantity : 2


Explanation:

| Register | Data |
|--------|--------|
0 | Humidity |
1 | Temperature |

---

# Example Sensor Response

Example response:
0292 FF9B


Humidity register:
0x0292 = 658
Humidity = 65.8 %RH

Temperature register:
0xFF9B = -101
Temperature = -10.1 °C


Both values are scaled by **10**.

---

# Step 3 — How to Detect Sensor Baudrate

Sometimes the baudrate is unknown.

The easiest way is to try common Modbus baudrates:
9600
19200
38400
115200


Once the correct baudrate is selected, the sensor will start responding.

---

# Step 4 — Change Modbus Slave ID

The slave address can be modified using **Function Code 06 (Write Single Register)**.

Configuration register:
Register : 0x0066

Example command:
01 06 00 66 00 02

This changes the device address:
Slave ID 1 → Slave ID 2

In Modbus Poll:
Function : 06
Address : 102
Value : 2

After writing, reconnect using the new Slave ID.

---

# Step 5 — Change Baudrate

Baudrate configuration register:
Register : 0x0067

Available values:

| Value | Baudrate |
|------|----------|
1 | 2400 |
2 | 4800 |
3 | 9600 |
4 | 19200 |
5 | 38400 |
6 | 115200 |

Example:
01 06 00 67 00 02


This sets the baudrate to:
4800 bps

After changing the baudrate, reconnect Modbus Poll using the new speed.

---

# Troubleshooting RS485 Communication

If the sensor does not respond:

Check the following:

**1. RS485 A/B reversed**

Swap A and B wires.

**2. Wrong baudrate**

Try different baudrates.

**3. Wrong Slave ID**

Try address scanning.

**4. Missing ground reference**

Connect sensor ground to RS485 converter ground.

---

# Conclusion

Using **Modbus Poll**, engineers can quickly test and configure RS485 sensors such as the AGH3485 temperature and humidity transmitter.

Key steps include:

- Connecting using correct Modbus settings
- Reading holding registers
- Converting raw data to engineering units
- Changing Slave ID and baudrate

This workflow is essential for **industrial IoT development, automation systems, and environmental monitoring projects**.

---

# Author

Usman AR  
Industrial IoT Engineer  
Embedded Systems Developer  
C++ / Qt / RS485 / Modbus Systems
