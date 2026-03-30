---
title: "Bluetooth Low Energy (BLE) Tracking System using TI CC2650 (Asset Tracking Solution)"
excerpt: "Dalam project ini, saya mengembangkan Bluetooth Low Energy (BLE) Tracking System berbasis chip TI CC2650 sebagai bagian dari aktivitas Research & Development di PT Internex Indonesia.<br/><img src='/images/Custom-Industrial-Smart PLC-STM32.png'>"
collection: portfolio
---

🚀 Overview
======
Dalam era digitalisasi industri, kebutuhan untuk melakukan tracking aset secara real-time menjadi semakin penting, terutama untuk meningkatkan efisiensi operasional dan visibilitas aset.

Dalam project ini, saya mengembangkan Bluetooth Low Energy (BLE) Tracking System berbasis chip TI CC2650 sebagai bagian dari aktivitas Research & Development di PT Internex Indonesia.

Solusi ini dirancang sebagai sistem tracking dengan konsumsi daya rendah (low power), yang mampu digunakan untuk berbagai skenario seperti:

Asset tracking di warehouse
Indoor positioning system
Personnel tracking
Smart inventory management

🎯 Objectives
======
Tujuan utama pengembangan sistem ini:

Membangun sistem tracking berbasis BLE dengan konsumsi daya rendah
Mengembangkan komunikasi stabil antara device dan mobile app
Membuat solusi yang scalable untuk kebutuhan industri
Mengintegrasikan hardware embedded dengan aplikasi mobile

🏗️ System Architecture

1. Device Layer (BLE Tag)

Perangkat utama menggunakan:

Texas Instrument CC2650 (BLE SoC)
Battery-powered device (low power consumption)

Fungsi utama:

Broadcast signal (BLE advertising)
Mengirimkan identifier unik
Optimasi interval advertising untuk efisiensi daya
2. Mobile Application Layer

Aplikasi Android dikembangkan untuk:

Scanning BLE devices
Menampilkan data tracking
Mapping device berdasarkan RSSI (signal strength)
User interface untuk monitoring
3. Communication Layer
BLE (Bluetooth Low Energy)
Advertising & scanning mechanism
RSSI-based proximity estimation
4. Backend (Optional / Future Ready)
Cloud sync (optional)
Data logging
Asset monitoring dashboard

⚙️ Key Features

✅ Low Power Consumption

Menggunakan BLE sehingga device dapat berjalan dalam waktu lama hanya dengan battery kecil.

✅ Real-Time Detection

Mampu mendeteksi keberadaan device secara langsung melalui scanning BLE.

✅ Scalable Deployment

Dapat digunakan untuk banyak device dalam satu area (multi-tag system).

✅ Mobile Integration

Aplikasi Android sebagai interface utama untuk monitoring.

🧩 Technical Challenges & Solutions

1. Power Optimization

Challenge:
Device BLE harus hemat daya agar bisa digunakan dalam jangka panjang.

Solution:

Optimasi advertising interval
Low-power mode pada CC2650
Efisiensi firmware
2. Signal Stability (RSSI Fluctuation)

Challenge:
RSSI pada BLE tidak stabil dan terpengaruh lingkungan (tembok, interferensi, dll).

Solution:

Filtering nilai RSSI (averaging)
Kalibrasi jarak berdasarkan environment
Threshold-based detection
3. Multi Device Handling

Challenge:
Handling banyak device BLE dalam satu waktu.

Solution:

Efficient scanning algorithm
Device identification system (UUID filtering)
🛠️ Tech Stack
Hardware
Texas Instrument CC2650
BLE Module
Software
Code Composer Studio (Firmware)
Android Studio (Java)
BLE Protocol Stack
📈 Impact & Value

Project ini memberikan fondasi untuk berbagai solusi berbasis BLE:

📦 Asset tracking system
🏭 Warehouse monitoring
👷 Personnel tracking
📍 Indoor positioning system

Keunggulan utama:

Low cost implementation
Low power consumption
Flexible deployment
🔮 Future Development

Beberapa pengembangan lanjutan yang dapat dilakukan:

Integration ke cloud (Firebase / MQTT)
Dashboard web monitoring
BLE Gateway (ESP32 / Raspberry Pi)
Machine learning untuk positioning accuracy
Hybrid tracking (BLE + GPS)
💡 Personal Note

Project ini memperkuat keahlian saya dalam:

Embedded system (BLE firmware)
Wireless communication
Mobile app development
System integration (hardware ↔ software)

Dan menjadi dasar untuk pengembangan solusi IoT tracking system yang lebih kompleks dan scalable.
