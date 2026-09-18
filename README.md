<div align="center">

# 🍎 Mac Remote

### Ultra-Low Latency Wireless Trackpad, Keyboard & Live Screen Streamer for macOS from iOS (iPhone & iPad) & Android

<p align="center">
  <a href="README.md"><b>🇬🇧 English</b></a> •
  <a href="README.tr.md"><b>🇹🇷 Türkçe</b></a>
</p>

[![GitHub Release](https://img.shields.io/github/v/release/ibrahimtemur/mac-remote-app?style=for-the-badge&color=blue)](https://github.com/ibrahimtemur/mac-remote-app/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-macOS%20%7C%20iOS%20%7C%20Android-black?style=for-the-badge&logo=apple)](https://github.com/ibrahimtemur/mac-remote-app)
[![Wiki Documentation](https://img.shields.io/badge/Documentation-Wiki-orange?style=for-the-badge)](https://github.com/ibrahimtemur/mac-remote-app/wiki)

<br/>

Turn your **iPhone, iPad, or Android device** into a high-precision, hardware-level remote trackpad, media controller, keyboard, and crystal-clear display mirror for macOS — over both Local Wi-Fi (LAN) and Internet (WAN).

[Features](#-key-features) • [How It Works](#-how-it-works) • [Installation](#-installation) • [Security](#-security) • [Wiki](https://github.com/ibrahimtemur/mac-remote-app/wiki)

</div>

---

## 📸 Screenshots

<div align="center">
  <h3>🇬🇧 English Interface</h3>
  <table>
    <tr>
      <td align="center"><b>1. Mobile Discovery & Pairing</b></td>
      <td align="center"><b>2. Trackpad, Mirror & Quality Tiers</b></td>
      <td align="center"><b>3. macOS Server Control Panel</b></td>
    </tr>
    <tr>
      <td align="center" valign="top"><img src="screenshots/android_connection_en.png" alt="Connection Screen (EN)" width="230"/></td>
      <td align="center" valign="top"><img src="screenshots/android_trackpad_en.png" alt="Trackpad & Live Screen (EN)" width="230"/></td>
      <td align="center" valign="top"><img src="screenshots/mac_server_en.png" alt="macOS Server GUI (EN)" width="280"/></td>
    </tr>
  </table>

  <h3>🇹🇷 Türkçe Arayüz</h3>
  <table>
    <tr>
      <td align="center"><b>1. Cihaz Keşfi & Bağlantı</b></td>
      <td align="center"><b>2. Trackpad, Ekran & Kalite Menüsü</b></td>
      <td align="center"><b>3. macOS Sunucu Kontrol Paneli</b></td>
    </tr>
    <tr>
      <td align="center" valign="top"><img src="screenshots/android_connection_tr.png" alt="Bağlantı Ekranı (TR)" width="230"/></td>
      <td align="center" valign="top"><img src="screenshots/android_trackpad_tr.png" alt="Trackpad & Canlı Ekran (TR)" width="230"/></td>
      <td align="center" valign="top"><img src="screenshots/mac_server_tr.png" alt="macOS Sunucu GUI (TR)" width="280"/></td>
    </tr>
  </table>
</div>

---

## ✨ Key Features

- 🖱️ **Hardware-Level Trackpad Emulation:**
  - **Fluid Cursor Navigation:** macOS CoreGraphics synthetic event dispatching with sub-pixel precision.
  - **Natural Multi-Touch Gestures:** 1-finger tap (left click), 1-finger long press or 2-finger tap (right click), and 2-finger fluid scrolling (vertical & horizontal).
  - **Full Text Selection & Drag-and-Drop:** Native `kCGEventLeftMouseDragged` support via double-tap-and-drag gesture or the dedicated **"Select Text"** toggle button.
  - **Dock & Hot Corners Triggering:** Engineered with cursor velocity boundary events to seamlessly summon the macOS Dock and Mission Control / Hot Corners.
- 📺 **Dynamic Real-Time Screen Mirroring:**
  - Ultra-fast JPEG frame streaming powered by native ScreenCapture API (`mss`).
  - **4 Dynamic Resolution Tiers:** Switch on the fly between **800p** (Fast / Low Data), **1200p** (Balanced), **1600p** (Crisp Text / Coding), and **2200p** (Ultra HD Crystal Clear).
  - Fullscreen & auto-rotating landscape layout with floating touchpad drawer (adapted for both iPhone and iPad large displays).
  - Interactive cursor overlay toggle on the preview canvas.
- 🎵 **Dedicated Multimedia & System Control Bar:**
  - Play/Pause, Next Track, Previous Track.
  - 10-second fast-forward and 10-second rewind for media and video players.
  - Native system volume buttons (Volume Up, Volume Down, Mute).
- ⌨️ **Expandable Virtual Keyboard:**
  - Integrated soft keyboard with quick helper buttons: `␣ Space`, `⌫ Backspace`, `⏎ Enter`, and `Esc`.
  - Glitch-free, single-stroke text delivery (no double-character bugs).
- 🌐 **Zero-Config Networking & Remote Access:**
  - **Local Network (LAN):** Automatic server discovery via Bonjour / mDNS (`_macremote._tcp.local.`) on iOS (Network.framework `NWBrowser`) & Android (`NsdManager`).
  - **Internet Access (WAN):** Integrated self-hosted reverse tunnel option with QR code generation — control your Mac from anywhere over cellular or remote Wi-Fi without router port forwarding.
  - **Dynamic 4-Digit PIN Security:** Fast, tamper-resistant handshake authentication.
- 🍏 **Apple Developer ID Signed & Notarized:**
  - macOS application distributed as a clean, signed `.dmg` installer verified by Apple Notary service.

---

## 🏗️ Architecture & How It Works

```
┌─────────────────────────────────┐
│           Mobile Client         │
│  • iOS (SwiftUI / Network.fw)   │
│  • Android (Compose / OkHttp)   │
└────────────────┬────────────────┘
                 │
                 ├── 1. Bonjour Auto-Discovery (LAN: _macremote._tcp.local.)
                 ├── 2. 4-Digit PIN Handshake Authentication
                 ├── 3. JSON Control Commands (Touch, Gestures, Keys) ───► ┌───────────────────────────┐
                 │                                                         │       macOS Server        │
                 │                                                         │   (Python 3.9+ / PyQt6)   │
                 │                                                         ├───────────────────────────┤
                 │                                                         │ • Zeroconf Publisher      │
                 │                                                         │ • Asyncio WebSocket Server│
                 │                                                         │ • CoreGraphics (Quartz)   │
                 └── 4. Real-Time JPEG Display Mirroring ◄──────────────── │ • Native 'mss' Grabber    │
                                                                           └───────────────────────────┘
```

1. **Discovery & Pairing:**
   - When the macOS server starts, it broadcasts its presence across the local network via Zeroconf / Bonjour (`_macremote._tcp.local.`).
   - The iOS client (`NWBrowser`) and Android client (`NsdManager`) automatically detect the Mac.
   - The client sends an authentication handshake containing the 4-digit PIN displayed on the Mac GUI.
2. **Input Injection:**
   - Motion and touch events are transmitted over low-overhead JSON WebSocket packets.
   - The server converts these into macOS CoreGraphics Quartz events (`CGEventCreateMouseEvent`, `CGEventPost` at `kCGHIDEventTap` level), providing true system-wide hardware emulation.
3. **Screen Mirroring:**
   - Screen frames are captured at the selected target resolution and compressed into JPEG memory buffers, transmitted as binary WebSocket frames for direct GPU rendering on iOS and Android.

---

## 📥 Installation

### 🍏 macOS (Server)
1. Navigate to the [Releases](https://github.com/ibrahimtemur/mac-remote-app/releases/latest) page and download `MacRemote-v1.4.0.dmg`.
2. Open the DMG and drag **Mac Remote.app** into your `/Applications` folder.
3. **Accessibility & Screen Recording Permissions:**
   - Open **macOS System Settings** > **Privacy & Security** > **Accessibility**, and grant permission to Mac Remote.
   - Under **Screen Recording**, ensure Mac Remote is allowed for live display streaming.
4. Launch **Mac Remote**, click **Start Server**, and note the 4-digit PIN.

### 📱 iOS (iPhone & iPad Client)
1. Install Mac Remote from the App Store or TestFlight.
2. Ensure your iOS device is connected to the same Wi-Fi network as your Mac (or enter the WAN remote address / scan the on-screen QR code).
3. Select your Mac from the discovered list (or tap Connect / scan QR).
4. Enter the 4-digit PIN displayed on your Mac's screen and tap Connect.

### 🤖 Android (Client)
1. Download `MacRemote-Android-v1.4.0.apk` from the [Releases](https://github.com/ibrahimtemur/mac-remote-app/releases/latest) page or install via Google Play.
2. Open **Mac Remote**, tap your Mac from the auto-discovered list (or scan the QR code), enter the 4-digit PIN, and connect.

---

## 🔒 Security Architecture

- Dynamic random 4-digit PIN generated on every server startup.
- Unauthenticated clients are rejected from sending keystrokes or mouse events.
- LAN connections run directly over your local Wi-Fi network; no external relay required.
- WAN connections use an isolated self-hosted reverse TCP tunnel on dedicated cloud infrastructure.
- macOS server binaries are signed with an official Apple Developer ID and notarized by Apple.
- Read our full [Security Policy (SECURITY.md)](SECURITY.md) for responsible disclosure guidelines.

---

## 🗺️ Roadmap

- [x] Multi-touch gestures (Tap, Right Click, 2-Finger Scroll, Drag Selection)
- [x] Dynamic screen quality tiers (800p to 2200p)
- [x] WAN access via self-hosted reverse tunnel & QR code
- [x] Native iOS (iPhone & iPad) SwiftUI client
- [x] Apple Developer ID signing & Notarized macOS DMG installer
- [ ] Direct WebRTC P2P connection mode (see [ROADMAP.md](ROADMAP.md))
- [ ] Bluetooth LE fallback connection for offline environments
- [ ] Multi-monitor switcher on macOS
- [ ] Biometric (Face ID / Fingerprint) quick-unlock on mobile
- [ ] Audio streaming from Mac to mobile devices

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

<div align="center">
  <sub>Made with ❤️ for seamless Mac, iOS, and Android interoperability.</sub>
</div>
