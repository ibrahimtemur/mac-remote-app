# 🗺️ Mac Remote — Project Roadmap

This document outlines upcoming architectural enhancements, features, and platform-specific polish planned for future releases of Mac Remote.

---

## 🚀 Near-Term Roadmap (Post v1.4.0)

### 1. WebRTC P2P Direct Connection (High Priority)
- **Goal:** Replace reverse TCP tunnel (bore) with direct peer-to-peer WebRTC DataChannels for WAN mirroring and trackpad control.
- **Benefits:** Ultra-low latency (~5–20ms instead of 30–80ms relay latency), reduced VPS bandwidth requirements.
- **Architecture:** 
  - Lightweight signaling via WebSocket on Oracle Cloud VPS.
  - Public STUN (`stun:stun.l.google.com:19302`) + free TURN fallback (OpenRelay / Metered.ca).
  - Python `aiortc` backend on macOS + native WebRTC in Swift and Kotlin.

### 2. Camera-Based QR Code Auto-Connect
- **Goal:** Allow mobile clients (iOS / iPadOS / Android) to scan the WAN connection QR code displayed on the Mac app.
- **Details:** Automatically fills in the remote host address and initiates connection dialog with zero typing needed.

### 3. Adaptive Tablet Layout (iPadOS & Android Tablets)
- **Goal:** Optimize the connection and control screens for large screens (iPad, Android tablets, foldables).
- **Details:** Replace the single-column centered mobile view with a dual-pane or adaptive grid layout that takes full advantage of wide displays.

### 4. Cross-Platform Design System & Brand Harmony
- **Goal:** Unify the visual aesthetic between iOS (monochrome, system frosted glass) and Android (Material 3 dynamic color scheme) for a consistent brand presence.

---

## 📋 Changelog Milestones
- **v1.4.0:** Migrated WAN architecture from Ngrok to self-hosted Bore tunnel on Oracle Cloud Always Free VPS with integrated QR code display.
- **v1.3.0:** Fullscreen movable trackpad overlay, iPad full-width connection card, Notarized macOS universal DMG.
- **v1.2.0:** Live screen streaming, multi-language support (TR/EN), haptic feedback.
