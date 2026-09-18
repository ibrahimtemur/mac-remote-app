# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.4.0] - 2026-09-18

### Changed
- **WAN Architecture Overhaul (Bore Self-Hosted Reverse Tunnel):**
  - Removed single-developer hardcoded Ngrok dependency. Each Mac now dynamically establishes an isolated reverse TCP tunnel to a dedicated Oracle Cloud Always Free VPS running `bore server`.
  - Zero manual account configuration or tokens required from end-users.
  - Generates a real-time QR code directly on the macOS server control panel alongside the remote address string for instant mobile connection.
  - Client UI strings across iOS, iPadOS, and Android updated in both English and Turkish to replace Ngrok branding with generic, clear remote WAN connection terminology.
  - Added user-friendly connection failure handling if the tunnel server is temporarily unreachable.

---

## [1.3.0] - 2026-09-17

### Added
- **Movable Trackpad Overlay in Fullscreen Mode:**
  - Trackpad panel on iOS and Android can now be freely dragged to any corner of the screen when viewing macOS display in fullscreen.
  - Added double-tap reset gesture and central pill grab handle.
- **iPad Full-Width Connection Card:**
  - Expanded discovered Mac computer cards to utilize available tablet display width.
- **Apple Developer ID Notarized DMG Distribution:**
  - Automated deep codesigning and Apple Notary Service verification pipeline for seamless macOS installation without Gatekeeper warnings.

---

## [1.1.0] - 2026-09-11

### Added
- **Interactive Setup & Connection Guide (Android):**
  - Added a dedicated setup guide button next to the "Mac Remote" header on the initial connection screen.
  - Step-by-step modal explaining how to download the Mac app from GitHub Releases, how to install and grant macOS Accessibility permissions, and how to pair using LAN or Ngrok.
  - Quick action button to open GitHub Releases page directly in the mobile browser.
- **Bilingual Interface Support (English & Turkish):**
  - **Android Client:** Added instant language switch button (🇹🇷 TR / 🇬🇧 EN) to both the initial connection screen and the connected Trackpad control bar (next to the cursor visibility icon). Localized quality selector menus, touchpad panel headers, gesture guide hints, physical click/scroll buttons, media controls, and keyboard actions.
  - **macOS Server GUI:** Added a top-bar language selector (🇹🇷 Türkçe / 🇬🇧 English) dynamically localizing server status, Start/Stop buttons, Ngrok toggle, and accessibility permission status.
  - User language preference is automatically remembered and persisted across app restarts on both platforms.

### Fixed
- **macOS App Startup Delay:** Resolved a 60-second unresponsive freeze when interacting with UI elements (such as the language selector) on application launch by disabling `argv_emulation` in py2app configuration.

---

## [1.0.0] - 2026-09-11

### Added
- **Hardware-Level Trackpad Control:**
  - 1-finger move: Smooth mouse cursor navigation.
  - 1-finger tap: Left click.
  - 1-finger long press / 2-finger tap: Right click.
  - 2-finger drag: Fluid vertical and horizontal scrolling.
  - Double-tap and drag: Native text selection and window dragging (`kCGEventLeftMouseDragged`).
  - Dedicated "Select Text" toggle button for reliable multi-line selection.
- **Dynamic Screen Streaming:**
  - Ultra-low latency JPEG screen preview via WebSocket.
  - 4 dynamic resolution tiers: 800p (Fast), 1200p (Balanced), 1600p (Sharp Text), and 2200p (Ultra HD).
  - Preview cursor overlay toggle.
- **Media & System Controls:**
  - Play/Pause, Next track, Previous track.
  - 10-second fast-forward and rewind controls.
  - System volume control (Volume Up, Volume Down, Mute).
- **Integrated Virtual Keyboard:**
  - Expandable keyboard drawer with quick helper keys (Space, Backspace, Enter, Esc).
  - Direct full-text transmission without double-typing glitches.
- **Connectivity & Networking:**
  - Automatic local network discovery (LAN) via mDNS / Zeroconf (`_macremote._tcp.local.`).
  - Remote internet access (WAN) using automated Ngrok encrypted TLS tunnels.
  - 4-digit dynamic PIN handshake authentication.
- **DevOps & Architecture:**
  - Monorepo structure: `/mac-app` (Python 3.9+ / PyQt6) and `/android-app` (Kotlin / Jetpack Compose).
  - Automated CI build and multi-platform GitHub Release workflow.
