# 🔧 Troubleshooting & FAQ

<p align="center">
  <a href="Troubleshooting-and-FAQ"><b>🇬🇧 English</b></a> •
  <a href="Troubleshooting-and-FAQ-TR"><b>🇹🇷 Türkçe</b></a>
</p>


Here you will find solutions to the most common questions and issues encountered when using Mac Remote.

---

## ❓ Frequently Asked Questions

### Q1: My Android device cannot find my Mac automatically.
**Checklist:**
1. **Wi-Fi Check:** Verify that both your Mac and mobile phone are on the **exact same Wi-Fi network**.
2. **Guest Network / AP Isolation:** Some public or hotel Wi-Fi networks have *Client Isolation (AP Isolation)* enabled, preventing devices from communicating directly. If so, use the **WAN Tunnel** mode instead.
3. **macOS Firewall:**
   - Go to **System Settings > Network > Firewall**.
   - Ensure incoming connections to `Mac Remote.app` are allowed.
4. **Manual Connection:** You can always connect directly using your Mac's local IP address:
   - On Mac, check your IP in `System Settings > Network > Wi-Fi > Details` (e.g. `192.168.1.50`).
   - In the mobile app, enter: `ws://192.168.1.50:8765`.

---

### Q2: I am connected, but moving my finger doesn't move the Mac mouse.
**Cause:** macOS Accessibility permissions are missing or revoked.
**Solution:**
1. Open **System Settings > Privacy & Security > Accessibility**.
2. If `Mac Remote` is listed, turn the toggle **OFF and then ON again**.
3. If it is not listed, click the `+` button and add `/Applications/Mac Remote.app`.
4. Restart `Mac Remote.app`. The green indicator `✓ Accessibility: Granted` must appear.

---

### Q3: Why does WAN connection fail or show "WAN connection is currently unavailable"?
**Possible Causes:**
1. **Network Firewall:** Your local network might block outbound TCP connections on the tunnel port (7835).
2. **Server Connectivity:** The VPS relay might be undergoing brief routine maintenance.
3. **Local Server Stopped:** Ensure you have clicked **Start Server** on the Mac and verified that the remote address with port appears on screen.

---

### Q4: Is my data safe? Does Mac Remote record my keys?
**Answer: Absolutely safe.**
- Local connections (`ws://192.168.x.x:8765`) are strictly direct over your private home/office Wi-Fi.
- No analytics, trackers, telemetry, or server-side logging of keystrokes exist.
- WAN connections use an isolated, authenticated reverse TCP tunnel without storing any payload.
- The full source code is public and open-source under the MIT license.

