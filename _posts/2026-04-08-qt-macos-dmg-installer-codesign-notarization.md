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

Abstract
------
This document describes a complete workflow for packaging a Qt C++ application on macOS, starting from a compiled .app bundle and ending with a signed, notarized .dmg installer ready for distribution. The process includes dependency deployment using macdeployqt, application code signing, disk image creation, and Apple notarization.

The goal of this guide is to provide a practical and production-oriented reference that avoids common pitfalls in macOS application distribution, particularly issues related to Gatekeeper and developer verification.

1. Introduction
------
Distributing applications on macOS requires more than simply compiling source code into a runnable binary. Apple enforces strict security policies through Gatekeeper, which validates application origin and integrity before allowing execution.

For Qt-based applications built using CMake, additional steps are required to ensure that all dependencies are correctly bundled and that the final application is accepted by the operating system without warnings.

This guide presents a structured approach to:

- Preparing a Qt .app bundle
- Bundling required Qt frameworks
- Signing the application with a Developer ID
- Packaging the application into a .dmg installer
- Submitting the installer for Apple notarization
- Finalizing distribution with stapled notarization tickets

The workflow described here is based on real-world deployment practices and is suitable for production environments.

2. Prerequisites
------
Before proceeding, ensure that the following requirements are met:

- 2.1 Development Environment
- Qt (e.g., version 6.x)
- CMake-based project
- Successful build producing a .app bundle
- Xcode Command Line Tools installed

2.2 Apple Developer Requirements
- Active Apple Developer account
- Developer ID Application certificate installed in Keychain

2.3 Security Considerations

It is strongly recommended to use an App-Specific Password instead of your Apple ID password when performing notarization.

3. Build Output
------
After building the project using CMake, the expected output should be a macOS application bundle:

build/Tren.app

If the application has not yet been built:

- mkdir build
- cd build
- cmake ..
- cmake --build .

4. Deploying Qt Dependencies

Qt applications depend on multiple frameworks and plugins that are not embedded by default. The macdeployqt tool is used to bundle these dependencies into the .app package.

~/Qt/6.x.x/macOS/bin/macdeployqt Tren.app \
  -qmldir=/path/to/project \
  -always-overwrite \
  -verbose=1

The -qmldir parameter ensures that QML dependencies are detected and included. The -always-overwrite flag replaces any existing deployed libraries, which is useful when rebuilding the application.

At this stage, the .app bundle should be self-contained and ready for signing.

5. Code Signing the Application
------

Code signing is required for macOS to recognize the application as coming from a verified developer. Without this step, the system may block execution or display security warnings.

codesign --deep --force --verify --verbose=1 \
  --options runtime \
  --sign "Developer ID Application: <YOUR_COMPANY_NAME> (<TEAM_ID>)" \
  Tren.app

Sensitive information such as the company name and team identifier should not be exposed in public repositories. Use placeholders when sharing documentation.

6. Verifying the Signature
------

After signing, verification should be performed to confirm that the application is properly signed.

codesign --deep --strict --verify --verbose=1 Tren.app

If no errors are reported, the signing process is valid.

7. Preparing the Installer Structure
------

A disk image installer typically contains the application and a symbolic link to the system Applications folder. This allows users to install the application via drag-and-drop.

mkdir out
cp -R Tren.app out
ln -s /Applications out

The resulting folder structure will be used as the source for the .dmg file.

8. Creating the DMG Installer
------

The hdiutil tool is used to create a compressed disk image.

hdiutil create \
  -volname "Tren Installer" \
  -srcfolder out \
  -ov \
  -format UDZO \
  Tren-v1.0.0.dmg

The UDZO format produces a compressed image suitable for distribution.

9. Signing the DMG File
------

The generated .dmg file must also be signed to ensure integrity.

codesign --sign "Developer ID Application: <YOUR_COMPANY_NAME> (<TEAM_ID>)" \
  Tren-v1.0.0.dmg
  
10. Notarization Setup
------

Apple notarization requires authentication via notarytool. Credentials should be stored securely using the system keychain.

xcrun notarytool store-credentials "notary-profile" \
  --apple-id "<YOUR_APPLE_ID>" \
  --team-id "<TEAM_ID>" \
  --password "<APP_SPECIFIC_PASSWORD>"

Never include real credentials in public documentation. Always replace them with placeholders.

11. Submitting for Notarization
------

Submit the .dmg file to Apple for automated security checks:

xcrun notarytool submit "Tren-v1.0.0.dmg" \
  --keychain-profile "notary-profile" \
  --wait

The --wait flag ensures that the process completes before returning control to the terminal.

12. Stapling the Notarization Ticket
------

Once notarization is successful, the result must be attached to the .dmg file:

xcrun stapler staple "Tren-v1.0.0.dmg"

This allows the installer to pass verification even without an internet connection.

13. Testing the Installer
------

Before distribution, it is important to test the installer on a clean macOS system.

The recommended steps are:

Download the .dmg
Open the disk image
Drag the application to the Applications folder
Launch the application

If the process completes without warnings, the installer is ready for release.

14. Common Issues
------

Several common issues may arise during this process:

Application cannot be opened because it is from an unidentified developer
This typically indicates missing or invalid code signing.
Application is reported as damaged
Often caused by incorrect signing or missing notarization.
Missing Qt libraries at runtime
Indicates that macdeployqt did not properly bundle dependencies.
Notarization failure
Usually related to invalid credentials or unsigned components.

15. Automation Considerations
------

For production environments, it is advisable to automate this workflow using shell scripts or CI/CD pipelines. This ensures consistency and reduces the risk of human error.

A simplified automation script may include:

Dependency deployment
Code signing
DMG creation
Notarization submission
Stapling

Integration with build systems such as CMake (via custom targets) or GitHub Actions can further streamline the release process.

16. Conclusion
------

Packaging a Qt application for macOS distribution involves several non-trivial steps that go beyond compilation. Proper handling of dependencies, code signing, and notarization is essential to meet Apple’s security requirements and to provide a smooth experience for end users.

By following the workflow described in this document, developers can produce installers that are secure, compliant, and suitable for professional distribution.
