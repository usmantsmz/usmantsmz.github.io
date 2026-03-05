---
title: "ASAIR AGH3485 Temperature Sensor RS485 – Datasheet and Modbus Communication Guide"
collection: publications
category: technical-reference
permalink: /publication/asair-agh3485-datasheet-modbus-guide
excerpt: 'Complete datasheet reference and Modbus communication guide for the ASAIR AGH3485 RS485 temperature sensor, including register map, baudrate configuration, and slave ID settings.'
date: 2026-03-05
venue: 'Technical Documentation'
paperurl: '/files/datasheet/usmantsmz-Temperature-and-humidity-transmitter（RS485）-Oct-2025.pdf'
citation: 'Usman AR TSM. (2026). "ASAIR AGH3485 Temperature Sensor RS485 – Datasheet and Modbus Communication Guide." Technical Documentation.'
---

ASAIR AGH3485 Temperature Sensor – Datasheet & Modbus Guide

The ASAIR AGH3485 is an industrial-grade temperature sensor that uses RS485 communication with the Modbus RTU protocol.
This sensor is commonly used in industrial monitoring systems, IoT environmental monitoring, cold storage systems, and building automation.

This publication provides a reference to the original datasheet along with practical notes for reading sensor data using Modbus tools such as Modbus Poll.

Sensor Overview

Key features of the AGH3485:

Industrial RS485 Modbus RTU interface

High accuracy temperature measurement

Long distance communication (up to ~1200 m over RS485)

Configurable Slave ID

Configurable baudrate

Suitable for industrial automation and IoT systems

Typical applications:

Cold storage monitoring

Industrial environmental monitoring

Smart agriculture systems

IoT data logger devices

Default Communication Settings

Typical factory configuration:

Parameter	Value
Protocol	Modbus RTU
Interface	RS485
Default Baudrate	9600
Data Format	8N1
Default Slave ID	1
Reading Temperature Data

Temperature can be read using Modbus holding registers.

Example:

Register Address	Description
0x0000	Temperature value

The value returned is typically scaled by 10.

Example:

Register Value : 253
Actual Temperature = 25.3 °C
Reading Sensor Data Using Modbus Poll

Using Modbus Poll:

Connect the sensor via USB-RS485 converter

Open Modbus Poll

Configure serial port

Example settings:

Baudrate : 9600
Data Bits : 8
Parity : None
Stop Bits : 1
Slave ID : 1

Then read:

Function : 03 Read Holding Registers
Address  : 0
Length   : 1
Changing Slave ID

To change the slave ID:

Write to the Slave ID configuration register

Use Modbus function 06 (Write Single Register)

Example:

Register : 0x0001
Value    : 2

Sensor will restart with the new address.

Changing Baudrate

Baudrate configuration can also be modified via Modbus register.

Typical baudrate options:

Value	Baudrate
0	2400
1	4800
2	9600
3	19200

After changing the value, restart the sensor.

Datasheet Download

Full datasheet can be downloaded here:

📄 files/datasheet/usmantsmz-Temperature-and-humidity-transmitter（RS485）-Oct-2025.pdf

Practical Notes

During testing, the sensor works well with:

Industrial data loggers

PLC systems

Microcontrollers such as ESP32

RS485 to USB converters

The sensor is especially suitable for low-power remote monitoring devices and IoT telemetry systems.

Citation

If you reference this documentation, please cite:

Usman AR TSM. (2026).
ASAIR AGH3485 Temperature Sensor RS485 – Datasheet and Modbus Communication Guide.
