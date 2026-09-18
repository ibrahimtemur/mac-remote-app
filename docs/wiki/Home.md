# 🍏 Welcome to the Mac Remote Wiki

<p align="center">
  <a href="Home"><b>🇬🇧 English</b></a> •
  <a href="Home-TR"><b>🇹🇷 Türkçe</b></a>
</p>

**Mac Remote** is a zero-configuration, ultra-low latency remote control suite that turns your **iPhone, iPad, or Android device** into a powerful wireless trackpad, keyboard, and presentation controller for macOS.

Whether you are presenting slides across a conference room, relaxing on your couch watching movies, or working remotely, Mac Remote provides instant control with hardware-level precision and native macOS integration.

---

## 🚀 Key Highlights

- **⚡ Instant Discovery (Zero Setup):** Automatic Mac server detection on local Wi-Fi via mDNS / Bonjour protocols on both iOS (`NWBrowser`) and Android (`NsdManager`).
- **🖐️ Natural Multi-Touch Gestures:** Precise cursor gliding, two-finger scrolling, right-click, double-click drag, and text selection.
- **🖥️ Real-time Screen Streaming:** Live desktop screen preview with variable adaptive quality (Fast 800p up to Ultra 2200p).
- **⌨️ Integrated Keyboard & Shortcuts:** Full mobile keyboard input, space, backspace, enter, and special function keys.
- **🌐 Global Internet Access:** Optional built-in reverse tunnel via Bore (`ws://`) with real-time QR code generation for connecting outside your local network without port forwarding.
- **🔒 Privacy First & Apple Notarized:** All local communications stay within your LAN. The macOS server is signed with an official Apple Developer ID and notarized by Apple.
- **🌐 Bilingual UI:** Full native support for both **English** and **Turkish (Türkçe)** with persistent language preferences.

---

## 🗺️ Documentation Index

| Section | Description |
| :--- | :--- |
| [📦 **Installation & Setup**](Installation-and-Setup) | Step-by-step installation for macOS (DMG), iOS (App Store/TestFlight), and Android, plus permissions. |
| [🌐 **Remote Access & WAN Tunnel**](Remote-Access-and-WAN) | How to use external internet connectivity, reverse tunnels, and QR code pairing. |
| [🖐️ **Gestures & Controls**](Gestures-and-Controls) | Master touch gestures, keyboard actions, and presentation shortcuts. |
| [🔧 **Troubleshooting & FAQ**](Troubleshooting-and-FAQ) | Solutions for common connection issues, firewall blocks, and permissions. |
| [🏗️ **Architecture & Protocols**](Architecture-and-Development) | Deep dive into WebSocket JSON protocols, multi-platform architecture, and specifications. |

---

## 📱 Supported Platforms
- **macOS Host:** macOS Monterey (12.0) or later (Apple Silicon M1/M2/M3/M4 & Intel), distributed as an Apple Developer ID signed & notarized DMG.
- **iOS Client:** iOS 16.0 or later (native SwiftUI for iPhone & iPad).
- **Android Client:** Android 8.0 (API 26) through Android 16 (API 36+), including tablets & foldable devices.
