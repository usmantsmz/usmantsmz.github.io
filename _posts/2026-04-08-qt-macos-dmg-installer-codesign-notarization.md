---
title: 'Complete Guide: Build Qt C++ macOS Installer (.app to .dmg) with Code Signing & Notarization'
permalink: /qt-macos-dmg-installer-codesign-notarization
date: 2026-04-08
categories:
- Qt
- C++
- macOS
- DevOps
tags:
- qt
- cmake
- macos
- dmg
- codesign
- notarization
- apple
---

Introduction
------
Dalam dunia distribusi aplikasi macOS, membuat aplikasi berjalan di mesin developer saja tidak cukup. Agar aplikasi dapat digunakan oleh end-user secara profesional, aman, dan tanpa warning dari sistem Apple, kita harus melalui beberapa tahapan penting:

- Packaging aplikasi .app
- Bundling dependency Qt
- Code Signing dengan Developer ID
- Membuat installer .dmg
- Notarization oleh Apple
- Stapling untuk validasi offline

Tutorial ini akan membahas end-to-end pipeline untuk aplikasi Qt berbasis CMake hingga siap didistribusikan secara profesional.

🎯 Tujuan Tutorial

Setelah mengikuti panduan ini, Anda akan mampu:

Mengubah aplikasi Qt .app menjadi installer .dmg
Menghindari error seperti:
“App is damaged and can’t be opened”
“Developer cannot be verified”
Memenuhi standar distribusi Apple
Membuat installer siap production
🧰 Prerequisites

Pastikan environment Anda sudah memenuhi:

1. Software
Qt (contoh: Qt 6.5.3)
Xcode Command Line Tools
CMake project sudah build sukses
2. Apple Developer
Apple Developer Account aktif
Developer ID Application Certificate
3. Security Requirement

Gunakan:

App-Specific Password
BUKAN password utama Apple ID
🏗️ Step 1 — Build Project (.app)

Pastikan Anda sudah memiliki hasil build:

build/Tren.app

Jika belum, lakukan build dari CMake:

mkdir build && cd build
cmake ..
cmake --build .
📦 Step 2 — Deploy Qt Dependencies (macdeployqt)

Qt tidak otomatis include dependency. Gunakan macdeployqt:

~/Qt/6.x.x/macOS/bin/macdeployqt Tren.app \
  -qmldir=/path/to/your/project \
  -always-overwrite \
  -verbose=1
🔍 Penjelasan:
-qmldir → scan dependency QML
-always-overwrite → replace library lama
-verbose → debug
⚠️ Best Practice:
Jalankan di folder release build
Pastikan tidak ada missing library
🔐 Step 3 — Code Signing Application

Untuk distribusi luar App Store, gunakan Developer ID Application.

codesign --deep --force --verify --verbose=1 \
  --options runtime \
  --sign "Developer ID Application: <YOUR_COMPANY_NAME> (<TEAM_ID>)" \
  Tren.app
🔒 Contoh Aman (Disamarkan):
codesign --sign "Developer ID Application: PT Example Company (ABCDE12345)" Tren.app
🔍 Step 4 — Verify Code Signing

Validasi hasil signing:

codesign --deep --strict --verify --verbose=1 Tren.app

Jika sukses, tidak ada error.

📁 Step 5 — Persiapan Folder Installer
mkdir out
cp -R Tren.app out
🔗 Step 6 — Tambahkan Shortcut Applications
ln -s /Applications out
💡 Kenapa ini penting?

Agar user bisa:
➡️ Drag & drop ke folder Applications
➡️ UX seperti aplikasi profesional macOS

💿 Step 7 — Create DMG Installer
hdiutil create \
  -volname "Your App Installer" \
  -srcfolder out \
  -ov \
  -format UDZO \
  YourApp-v1.0.0.dmg
📌 Penjelasan:
UDZO → compressed image
-ov → overwrite
🔐 Step 8 — Code Sign DMG
codesign --sign "Developer ID Application: <YOUR_COMPANY_NAME> (<TEAM_ID>)" \
  YourApp-v1.0.0.dmg
☁️ Step 9 — Setup Notary Credentials (One-Time)

⚠️ Jangan expose credential asli di repo publik!

xcrun notarytool store-credentials "notary-profile" \
  --apple-id "<YOUR_APPLE_ID>" \
  --team-id "<TEAM_ID>" \
  --password "<APP_SPECIFIC_PASSWORD>"
🔒 Contoh Aman:
--apple-id "your-email@example.com"
--team-id "ABCDE12345"
--password "xxxx-xxxx-xxxx-xxxx"
📤 Step 10 — Submit ke Apple Notarization
xcrun notarytool submit "YourApp-v1.0.0.dmg" \
  --keychain-profile "notary-profile" \
  --wait
⏳ Proses:
Upload ke Apple
Scan malware
Validasi signature
📎 Step 11 — Staple Notarization
xcrun stapler staple "YourApp-v1.0.0.dmg"
🎯 Tujuan:

Menambahkan tiket notarization ke file agar:

Bisa digunakan offline
Tidak perlu check ulang ke server Apple
🧪 Step 12 — Testing (PENTING)

Test di Mac lain (clean system):

Download DMG
Open
Drag ke Applications
Run
❌ Jika gagal:
“App is damaged” → signing salah
“Cannot verify developer” → notarization gagal
🧠 Deep Understanding (Advanced Insight)
🔹 Kenapa Harus Codesign?

Apple Gatekeeper akan:

Block aplikasi unsigned
Warning ke user
🔹 Kenapa Notarization?

Apple ingin memastikan:

Tidak ada malware
Developer terverifikasi
🔹 Kenapa Staple?

Tanpa staple:

macOS perlu internet untuk validasi
⚙️ Automation (Recommended for Production)

Daripada manual, buat script:

#!/bin/bash

APP="Tren.app"
DMG="Tren-v1.0.0.dmg"
CERT="Developer ID Application: <YOUR_COMPANY> (<TEAM_ID>)"

macdeployqt $APP -qmldir=.

codesign --deep --force --options runtime --sign "$CERT" $APP

mkdir -p out
cp -R $APP out
ln -s /Applications out

hdiutil create -volname "Installer" -srcfolder out -ov -format UDZO $DMG

codesign --sign "$CERT" $DMG

xcrun notarytool submit $DMG --keychain-profile "notary-profile" --wait
xcrun stapler staple $DMG
🚨 Common Pitfalls
❌ 1. Hardcode Password di Repo

➡️ SOLUSI: gunakan keychain / env variable

❌ 2. Missing Qt Library

➡️ SOLUSI: cek macdeployqt

❌ 3. Salah Certificate

➡️ Gunakan:

Developer ID Application (bukan Mac Developer)
❌ 4. Tidak Notarize

➡️ User akan dapat warning

🔥 Pro Tips dari Experience
Gunakan CI/CD untuk build otomatis
Versioning wajib konsisten
Gunakan custom DMG UI (background, icon)
Hindari --deep untuk production advanced (manual signing lebih clean)
🎯 Conclusion

Dengan mengikuti pipeline ini:

✅ Aplikasi Anda terlihat profesional
✅ Aman dari Gatekeeper
✅ Trusted oleh Apple
✅ Siap distribusi ke client / user

🚀 Next Level (Optional Upgrade)

Jika ingin lebih advanced, Anda bisa:

Integrasi ke CMake (CPack)
Custom UI DMG (drag arrow, background image)
Auto build via GitHub Actions
OTA update system
📢 Call To Action

Jika Anda butuh:

Jasa build installer macOS profesional
Setup CI/CD Qt project
Integrasi signing & notarization
Development aplikasi Qt (Trading, IoT, Desktop)

Silakan hubungi saya — saya sudah berpengalaman di:

High performance Qt apps
Financial & trading system
Industrial & IoT platform
