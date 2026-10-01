<div align="center">

# 🛡️ MC-ExamBrowser
### Enterprise-Grade Multiplatform Kiosk Client for Computer-Based Testing (CBT)

[![GitHub Release](https://img.shields.io/badge/release-v2.4.0-0284c7?style=for-the-badge&logo=github)](https://github.com/maulanacod3/MC-ExamBrowser/releases/latest)
[![Platform - Android](https://img.shields.io/badge/platform-Android_7.0+-10b981?style=for-the-badge&logo=android)](https://github.com/maulanacod3/MC-ExamBrowser/releases/latest)
[![Platform - Windows](https://img.shields.io/badge/platform-Windows_10%20%2F%2011-0078d7?style=for-the-badge&logo=windows)](https://github.com/maulanacod3/MC-ExamBrowser/releases/latest)
[![Security - Kiosk Mode](https://img.shields.io/badge/security-Kernel_Level_Lockdown-6366f1?style=for-the-badge&logo=shield)](https://mcode.web.id/exambrowser)
[![License - Commercial / Free](https://img.shields.io/badge/license-MCode_Proprietary-f59e0b?style=for-the-badge)](https://mcode.web.id)

<p align="center">
  <strong>The official lockdown browser designed for schools, universities, and certification institutions across Indonesia.</strong><br>
  Eliminates cheating vectors: multitasking, floating AI assistants, remote desktop jockeying, screen recording, and unauthorized network routing.
</p>

[Official Website](https://mcode.web.id/exambrowser) • [Latest Downloads](https://github.com/maulanacod3/MC-ExamBrowser/releases/latest) • [Proctor Guide](#-proctor-emergency-guide) • [School Deployment](#-mass-deployment-guide)

---

</div>

## 📌 Executive Summary

**MC-ExamBrowser** is a high-security CBT client available for **Android devices** (smartphones, tablets, and Chromebooks) and **Windows Desktop PCs** (standalone laptops and school computer laboratories). 

Unlike conventional browser wrappers, MC-ExamBrowser operates directly at the operating system and window management level:
- **Android:** Utilizing Android Device Administration, Accessibility & Display Manager APIs to enforce hard kiosk lockdowns.
- **Windows (.NET 8 WPF & Edge WebView2):** Utilizing low-level Win32 hooks (`WH_KEYBOARD_LL`), Windows Display Affinity (`WDA_EXCLUDEFROMCAPTURE`), and process watchdog daemons.

---

## 🔒 Core Security Pillars

| Security Vector | Android Mobile Engine | Windows Desktop Engine (.NET 8) |
|---|---|---|
| **Navigation Lock** | Hardware Screen Pinning, blocks Home, Back, Recents | Hooks `Alt+Tab`, `Alt+F4`, `Win Key`, `Win+D`, `Win+Shift+S` |
| **Task Manager Guard** | Blocks Settings, App Switcher, and Split-Screen | Enforces Registry Policy `DisableTaskMgr = 1` during session |
| **Anti-Screen Capture** | `FLAG_SECURE` blocks screenshots & screen recording | `SetWindowDisplayAffinity` produces pure black screen in OBS/Discord/Zoom |
| **Anti-Remote Jockey** | Blocks Developer Options, Mock Locations & ADB | Real-time daemon terminates AnyDesk, TeamViewer, RustDesk & `OSK.exe` |
| **Strict Local Network** | Restricts traffic strictly to designated school LAN / SSID | Enforces school intranet IP whitelist & blocks public mobile data |
| **AI Floating Widgets** | Auto-kills floating chat bubbles & AI overlay apps | Sandboxed Chromium engine isolates browser DOM & scripts |
| **AI Proctoring** | CameraX & ML Kit on-device head pose & multi-face alarm | Dual Monitor / HDMI intercept locks screen if secondary display attached |
| **Configuration Tamper** | Instant QR Scan + Encrypted `.mcode` sidecar file | AES-256 encrypted `config.mcode` verified by `HMAC-SHA256` signature |

---

## 📥 Official Download Links

Pre-compiled binary releases are distributed exclusively via GitHub CDN for fast and reliable distribution:

| Platform | Type | Architecture | Minimum OS | Download Link |
|---|---|---|---|---|
| **Android APK** | Universal APK | `arm64-v8a`, `armeabi-v7a`, `x86_64` | Android 7.0 (Nougat) s/d Android 15+ | [📦 Download APK (v2.4.0)](https://github.com/maulanacod3/MC-ExamBrowser/releases/latest/download/mc-exambrowser.apk) |
| **Windows Setup** | Installer `.exe` | `x64` (64-bit) | Windows 10 / 11 | [💻 Download Setup (v1.0.0)](https://github.com/maulanacod3/MC-ExamBrowser/releases/latest/download/MCExamBrowser.exe) |
| **Windows Portable** | Standalone `.zip` | `x64` (64-bit Lab Ready) | Windows 10 / 11 | [⚡ Download Portable .zip](https://github.com/maulanacod3/MC-ExamBrowser/releases/latest/download/MCExamBrowser-Windows.zip) |

> 💡 **Mirror Cloud & Release Archive:**  
> All historical releases and mirror downloads can be accessed directly on the [GitHub Releases Page](https://github.com/maulanacod3/MC-ExamBrowser/releases).

---

## 🏫 Mass Deployment Guide (Computer Labs)

For school computer laboratories managing 40–100+ desktop workstations, use the **Quick Config Studio** zero-configuration strategy:

### Directory Structure
Extract the standalone bundle into a shared LAN folder or flash drive:
```text
📁 MCExamBrowser-Lab/
├── ⚙️ MCExamBrowser.exe       # Portable Kiosk Executable (.NET 8 WPF)
├── 📄 app.manifest            # High-DPI PerMonitorV2 scaling configuration
└── 🔒 config.mcode            # AES-256 encrypted CBT server settings
```

### 3-Step Lab Setup:
1. **Generate Configuration:**  
   Open `MCExamBrowser.exe` on the proctor's master PC, enter the school CBT URL, set proctor exit password, and click **`[ 📤 Ekspor .mcode ]`**.
2. **Distribute File:**  
   Copy the generated `config.mcode` sidecar file into the same directory as `MCExamBrowser.exe` across all student lab computers (via Flashdisk, Shared Network Drive `\\server\cbt`, or NetSupport / Veyon broadcast).
3. **Launch & Auto-Lock:**  
   When student workstations launch `MCExamBrowser.exe`, it automatically reads and decrypts `config.mcode`, immediately enforcing full kiosk security.

---

## 👨‍🏫 Proctor Emergency Guide

In case a student device freezes or requires emergency proctor intervention:

### Master Rescue PIN: `098123`

Proctors have three access methods to open the **Proctor Override Modal**:
1. **Secret Keyboard Shortcut:** Press <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>F12</kbd> on the student's keyboard.
2. **Logo Gesture:** Click the school title located in the top-left status bar **5 times consecutively** within 2 seconds.
3. **Freeze Screen Action:** Click the purple **"Buka Kunci Pengawas"** button on the penalty freeze screen.

### Proctor Override Capabilities:
- 🔓 **Bypass Freeze:** Immediately cancels screen penalty and restores student integrity score to 100%.
- 🔗 **Live URL Switch:** Updates CBT server IP/URL on the fly without closing the client (ideal for LAN failovers).
- 🚪 **Emergency Exit:** Cleanly shuts down the kiosk sandbox, restoring Windows Task Manager and system policies.

---

## 🚪 Passwordless SEB Exit Protocol

MC-ExamBrowser natively supports the standard Safe Exam Browser (SEB) exit specification. When students complete their test, the exam portal can trigger any of the following URL schemes:
- `seb://quit`
- `sebs://quit`
- `mc://quit`
- `window.close()`

Upon receiving this signal, the browser automatically prompts confirmation and exits gracefully **without requesting teacher intervention or password entry**.

---

## 🌐 Ecosystem Integration

MC-ExamBrowser connects seamlessly with any web-based CBT or LMS platform:
- **[MC-ExamGO](https://mcode.web.id/examgo):** Ultra high-performance Go + PostgreSQL CBT engine (5,000+ concurrent students).
- **Moodle LMS:** Full support for quiz lockdown and Safe Exam Browser access tokens.
- **Candy CBT / BeeSMART / Google Forms:** Zero-effort compatibility via custom domain whitelisting.

---

## 📞 Support & Community

- **Official Web Portal:** [https://mcode.web.id](https://mcode.web.id)
- **Technical Support & Licensing:** WhatsApp [+62 812-3456-7890](https://wa.me/6281234567890)
- **Issue Tracker:** [GitHub Issues](https://github.com/maulanacod3/MC-ExamBrowser/issues)

---

<div align="center">
  <small>© 2026 MCode Technology. All rights reserved. Proprietary software — binary distribution authorized under MCode Educational Terms.</small>
</div>
