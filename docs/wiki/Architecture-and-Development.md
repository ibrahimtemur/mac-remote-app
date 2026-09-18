# 🏗️ Architecture & Protocols Specification

<p align="center">
  <a href="Architecture-and-Development"><b>🇬🇧 English</b></a> •
  <a href="Architecture-and-Development-TR"><b>🇹🇷 Türkçe</b></a>
</p>

This document details the internal multi-platform architecture, network protocols, and data structures for Mac Remote.

---

## 🏛️ System Overview

```mermaid
graph TD
    subgraph iOS App ["iOS Client (SwiftUI)"]
        iOS_UI[Touchpad Screen / Gestures]
        iOS_Discovery[Bonjour Browser (Network.framework)]
        iOS_WS[WebSocketClient (URLSessionWebSocketTask)]
        iOS_UI --> iOS_WS
        iOS_Discovery --> iOS_WS
    end

    subgraph Android App ["Android Client (Jetpack Compose)"]
        Droid_UI[Touchpad Screen / Gestures]
        Droid_Discovery[DiscoveryManager (mDNS NsdManager)]
        Droid_WS[WebSocketClient (OkHttp)]
        Droid_UI --> Droid_WS
        Droid_Discovery --> Droid_WS
    end

    subgraph macOS Host ["macOS Server (PyQt6 + Asyncio)"]
        WSServer[WebSocket Server (Port 8765)]
        mDNS[Zeroconf / Bonjour Service (_macremote._tcp)]
        InputCtrl[Input Controller (CoreGraphics & Quartz)]
        ScreenCap[Screen Capture (MSS / CoreGraphics)]
        Tunnel[Bore Isolated Reverse Tunnel (VPS)]
        
        WSServer --> InputCtrl
        WSServer --> ScreenCap
        Tunnel -.-> WSServer
    end

    iOS_WS <==>|JSON Messages + Binary JPEG Frames| WSServer
    Droid_WS <==>|JSON Messages + Binary JPEG Frames| WSServer
```

---

## 📡 WebSocket Protocol Specification

All control communications between mobile clients and the macOS server occur over a persistent WebSocket connection (`ws://` on LAN or `ws://` via dedicated WAN reverse tunnel) on port **8765** using lightweight JSON payloads:

### 1. Authentication Handshake
```json
{
  "type": "auth",
  "pin": "4530"
}
```

### 2. Relative Mouse Move
```json
{
  "type": "mouse_move",
  "dx": 12.5,
  "dy": -4.2
}
```

### 3. Mouse Clicks & Dragging
- Left Click: `{"type": "mouse_click", "button": "left"}`
- Right Click: `{"type": "mouse_click", "button": "right"}`
- Drag Begin: `{"type": "mouse_drag_begin"}`
- Drag Move: `{"type": "mouse_drag_move", "dx": 10.0, "dy": 5.0}`
- Drag End: `{"type": "mouse_drag_end"}`

### 4. Scrolling
```json
{
  "type": "mouse_scroll",
  "dx": 0.0,
  "dy": 3.5
}
```

### 5. Keyboard Input
```json
{
  "type": "key_press",
  "key": "enter"
}
```

### 6. Media Controls
```json
{
  "type": "media_control",
  "action": "play_pause"
}
```
*(Supported actions: `play_pause`, `next`, `previous`, `volume_up`, `volume_down`, `mute`, `forward_10s`, `rewind_10s`)*

### 7. Dynamic Screen Stream Tiers
```json
{
  "type": "set_quality",
  "quality": "1600p"
}
```
*(Available tiers: `800p`, `1200p`, `1600p`, `2200p`)*
