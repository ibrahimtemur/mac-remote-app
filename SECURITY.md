# Security Policy

## ⚠️ Security Overview for Mac Remote

Because **Mac Remote** provides hardware-level remote control capabilities (mouse emulation, keystrokes, screen capturing, and system shortcuts) over your Mac from an Android device, security and responsible disclosure are our highest priorities.

---

## 🛡️ Supported Versions

We release patches and security fixes for the following versions:

| Version | Supported          |
| ------- | ------------------ |
| 1.0.x   | :white_check_mark: |
| < 1.0   | :x:                |

---

## 🔒 Security Architecture & Best Practices

1. **PIN Authentication:**
   - Every connection session requires a dynamic 4-digit PIN generated on the Mac server GUI.
   - Unauthenticated clients cannot control the cursor, send keystrokes, or view the screen feed.

2. **Network Boundaries:**
   - **Local Area Network (LAN):** By default, Mac Remote operates strictly on your private local network via mDNS and WebSocket (`ws://`). Never expose port `8765` directly to the public internet without an encrypted tunnel.
   - **Remote Internet Access (WAN Tunnel):** When enabled, traffic is tunneled through an isolated, authenticated reverse TCP tunnel (Bore) hosted on private cloud infrastructure. Each session requires dynamic 4-digit PIN authentication. Never share your remote address or PIN with untrusted parties.

3. **macOS Accessibility Sandbox:**
   - The Mac server requires explicit user approval under **macOS System Settings > Privacy & Security > Accessibility** to dispatch synthetic input events. It does not circumvent or alter macOS security boundaries.

---

## 🚨 Reporting a Vulnerability

If you discover a security vulnerability or concern within Mac Remote:

1. **DO NOT** disclose the issue publicly (e.g., via GitHub Issues, public tweets, or forums) before it has been addressed.
2. Please submit a confidential report via **GitHub Security Advisories** (found under the `Security` tab of the repository) or contact the project maintainers directly.
3. Include detailed steps to reproduce the issue, proof of concept (PoC), and affected versions/platforms.
4. We acknowledge receipt within **48 hours** and aim to provide an update or patch within **7 business days**.
