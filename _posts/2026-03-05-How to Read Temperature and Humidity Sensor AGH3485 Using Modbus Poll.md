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
