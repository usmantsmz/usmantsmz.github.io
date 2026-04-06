---
layout: archive
title: "Curriculum Vitae"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

## 👨‍💻 Profile
Senior Software Engineer & IoT Specialist dengan pengalaman dalam pengembangan sistem embedded, industrial automation, dan integrasi IoT end-to-end.

Berpengalaman dalam membangun:
- Sistem monitoring berbasis sensor & cloud
- Aplikasi desktop (C++ Qt)
- Firmware embedded (ESP32, STM32)
- Integrasi Modbus, MQTT, dan protokol industri lainnya

Fokus utama pada **reliability, scalability, dan real-world deployment**.

---

## 🎓 Education
- **Sarjana Teknik (S.T)** – Teknik Elektro / Informatika  
  *(Sesuaikan dengan kampus lo)*  

---

## 💼 Work Experience

### 🔹 Senior Software Engineer & IoT Developer (Freelance / Project-Based)
**2020 – Present**

- Develop sistem monitoring IoT berbasis ESP32 + sensor industrial
- Integrasi Modbus RTU/TCP dengan PLC & perangkat lapangan
- Build data pipeline ke cloud (MQTT, REST API, ThingsBoard)
- Develop dashboard monitoring (Web & Desktop)
- Implementasi OTA firmware & remote device management
- Design sistem logging berbasis SD Card & server

---

### 🔹 Embedded System & Automation Engineer
**Project Industrial & Research**

- Development firmware untuk:
  - Water level monitoring
  - Weather station (angin, hujan, suhu, tekanan)
  - Soil sensor & environmental monitoring
- Integrasi RS485 multi-device dalam satu sistem
- Optimasi komunikasi serial (multi baudrate, parity handling)
- Fail-safe & anti-hang system design untuk device lapangan

---

### 🔹 Desktop Application Developer (C++ Qt)
**Freelance / Personal Project**

- Develop aplikasi desktop untuk:
  - Monitoring device IoT
  - Serial communication tools
  - Data visualization & logging
- Implementasi UI/UX berbasis Qt Widgets & Qt Quick
- Integrasi backend C++ dengan hardware interface

---

## 🛠️ Skills

### 🔧 Programming
- C / C++
- Python
- JavaScript (Basic)
- Embedded C

### ⚙️ Embedded & Hardware
- ESP32 / ESP32-S3
- STM32 (Basic)
- Arduino Platform
- Sensor Integration (I2C, UART, ADC)

### 🌐 Communication Protocol
- Modbus RTU / TCP
- MQTT
- HTTP / REST API
- Serial RS232 / RS485

### 💻 Software & Tools
- Qt Creator (C++ Desktop App)
- VS Code / PlatformIO
- Git & GitHub
- Linux (Ubuntu Server)

### ☁️ IoT & Backend
- ThingsBoard
- Custom IoT Dashboard
- Data Logging System
- OTA Firmware Update System

---

## 🚀 Selected Projects

### 🔹 IoT Weather Monitoring System
- Sensor: angin, hujan, suhu, tekanan
- ESP32 + SD Card Logging
- Kirim data ke cloud via MQTT
- Real-time dashboard monitoring

---

### 🔹 Smart Water Level Monitoring
- Sensor submersible + Modbus
- Auto calibration (zero offset)
- Logging + remote monitoring
- Anti-hang & fail-safe firmware

---

### 🔹 Multi-Sensor RS485 Integration System
- Soil sensor, rain gauge, water level
- Multi-device dalam 1 bus RS485
- Dynamic serial config (baudrate & parity)
- Stabil untuk deployment lapangan

---

### 🔹 Custom Desktop Monitoring App (Qt C++)
- Serial communication tool
- Real-time data visualization
- Digunakan untuk debugging & monitoring device

---

## 📚 Publications
<ul>
{% for post in site.publications reversed %}
  {% include archive-single-cv.html %}
{% endfor %}
</ul>

---

## 🎤 Talks & Sharing
<ul>
{% for post in site.talks reversed %}
  {% include archive-single-talk-cv.html %}
{% endfor %}
</ul>

---

## 🧑‍🏫 Teaching & Mentoring
<ul>
{% for post in site.teaching reversed %}
  {% include archive-single-cv.html %}
{% endfor %}
</ul>

---

## 🤝 Service & Collaboration

- Open to collaboration on:
  - IoT Development
  - Embedded System Project
  - Industrial Automation
- Aktif dalam pengembangan project berbasis real-world deployment

---

## 📫 Contact

- 🌐 Website: https://sayuswa.com  
- 💼 GitHub: https://usmantsmz.github.io/  
- 📧 Email: usmanar.tsm@gmail.com  

---

## 💡 Notes

Sebagian besar pengalaman saya berasal dari implementasi langsung di lapangan, bukan hanya simulasi atau prototype. Fokus utama adalah membangun sistem yang:

- Stabil dalam jangka panjang  
- Tahan terhadap kondisi lingkungan  
- Mudah di-maintain dan scalable  
