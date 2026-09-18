# 🏗️ Mimari & Protokol Özellikleri

<p align="center">
  <a href="Architecture-and-Development"><b>🇬🇧 English</b></a> •
  <a href="Architecture-and-Development-TR"><b>🇹🇷 Türkçe</b></a>
</p>

Bu belge, Mac Remote'un çok platformlu iç mimarisini, ağ protokollerini ve veri yapılarını ayrıntılı olarak açıklar.

---

## 🏛️ Sisteme Genel Bakış

```mermaid
graph TD
    subgraph iOS İstemci ["iOS İstemcisi (SwiftUI)"]
        iOS_UI[Touchpad Ekranı / Hareketler]
        iOS_Discovery[Bonjour Tarayıcı (Network.framework)]
        iOS_WS[WebSocketClient (URLSessionWebSocketTask)]
        iOS_UI --> iOS_WS
        iOS_Discovery --> iOS_WS
    end

    subgraph Android İstemci ["Android İstemcisi (Jetpack Compose)"]
        Droid_UI[Touchpad Ekranı / Hareketler]
        Droid_Discovery[Keşif Yöneticisi (mDNS NsdManager)]
        Droid_WS[WebSocketClient (OkHttp)]
        Droid_UI --> Droid_WS
        Droid_Discovery --> Droid_WS
    end

    subgraph macOS Sunucu ["macOS Sunucusu (PyQt6 + Asyncio)"]
        WSServer[WebSocket Sunucusu (Port 8765)]
        mDNS[Zeroconf / Bonjour Yayını (_macremote._tcp)]
        InputCtrl[Girdi Yöneticisi (CoreGraphics & Quartz)]
        ScreenCap[Ekran Yakalama (MSS / CoreGraphics)]
        Tunnel[Bore İzole Ters Tünel (VPS)]
        
        WSServer --> InputCtrl
        WSServer --> ScreenCap
        Tunnel -.-> WSServer
    end

    iOS_WS <==>|JSON Mesajları + İkili JPEG Kareleri| WSServer
    Droid_WS <==>|JSON Mesajları + İkili JPEG Kareleri| WSServer
```

---

## 📡 WebSocket Protokol Tanımı

Mobil istemciler ile macOS sunucusu arasındaki tüm kontrol iletişimi, **8765** portu üzerinden kalıcı bir WebSocket bağlantısı (`ws://` yerel ağda veya WAN tüneliyle `ws://`) ve hafif JSON yükleriyle gerçekleşir:

### 1. Kimlik Doğrulama El Sıkışması
```json
{
  "type": "auth",
  "pin": "4530"
}
```

### 2. Bağıl Fare Hareketi
```json
{
  "type": "mouse_move",
  "dx": 12.5,
  "dy": -4.2
}
```

### 3. Tıklama ve Sürükleme
- Sol Tık: `{"type": "mouse_click", "button": "left"}`
- Sağ Tık: `{"type": "mouse_click", "button": "right"}`
- Sürükleme Başlangıcı: `{"type": "mouse_drag_begin"}`
- Sürükleme Hareketi: `{"type": "mouse_drag_move", "dx": 10.0, "dy": 5.0}`
- Sürükleme Bitişi: `{"type": "mouse_drag_end"}`

### 4. Kaydırma
```json
{
  "type": "mouse_scroll",
  "dx": 0.0,
  "dy": 3.5
}
```

### 5. Klavye Girişi
```json
{
  "type": "key_press",
  "key": "enter"
}
```

### 6. Medya ve Ses Kontrolleri
```json
{
  "type": "media_control",
  "action": "play_pause"
}
```
*(Desteklenen eylemler: `play_pause`, `next`, `previous`, `volume_up`, `volume_down`, `mute`, `forward_10s`, `rewind_10s`)*

### 7. Dinamik Ekran Kalite Kademeleri
```json
{
  "type": "set_quality",
  "quality": "1600p"
}
```
*(Seçenekler: `800p`, `1200p`, `1600p`, `2200p`)*
