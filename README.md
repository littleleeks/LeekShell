# LeekShell

> Lightweight, fully self-developed C2 — a new choice for red teams | Tested: Kaspersky Premium + EDR both blinded


**LeekShell** is a completely self-developed lightweight C2 framework built with a **Python + C++** architecture. It discards some redundant features in exchange for higher stealth and controllability.

The signatures of Cobalt Strike, Sliver, and Havoc on the market have been thoroughly dissected by security vendors. Even with modified profiles or secondary development of the beacon, they struggle against antivirus and EDR. Thus, this fully self-developed C2 framework — **LeekShell (Version 1)** — was born.

> **Reason for not open-sourcing**: The author is based in China, and this tool is intended solely for learning, research, and legally authorized use. The source code is not public to prevent malicious exploitation and to protect the author and users.

---

## 📌 Table of Contents

- [Antivirus Evasion Test Results](#-antivirus-evasion-test-results)
- [Usage Guide](#-usage-guide)
- [Quick Start](#-quick-start)
- [Why Build a New C2?](#-why-build-a-new-c2)
- [Disclaimer](#-disclaimer)

---

## 🛡️ Antivirus Evasion Test Results

| Security Product | Version | Test Result |
|---------|------|----------|
| **Kaspersky Premium** | June 2026 latest signature database | ✅ Successful beacon, command execution successful, no pop-ups or blocks throughout |
| **Kaspersky Endpoint Detection and Response** (Kaspersky EDR) | June 2026 latest signature database | ✅ Successful beacon, commands such as `whoami`, `ipconfig`, `tasklist` returned normal output, no high-risk alerts in EDR console |

> Test environment: Windows 10 21H2, Kaspersky fully updated to the latest June 2026 signature database.

---
### Kaspersky Premium:

<img width="1632" height="729" alt="685dcf87c5b1500adab5562360a6fee7" src="https://github.com/user-attachments/assets/fcc81702-67dd-4148-a5a6-53629b88ad1b" />
<img width="948" height="600" alt="68f7b7478ec5e56997106f8b54a6995c" src="https://github.com/user-attachments/assets/b6ce0559-1a9a-4b43-82e0-9ef369eed655" />
<img width="1842" height="699" alt="faa35c805c5de2bb197c677b2e0f5879" src="https://github.com/user-attachments/assets/cb1da435-3cf4-46a7-a1c3-4d6d19779f11" />

### Kaspersky EDR:
<img width="1515" height="584" alt="cd6c9a2c1af8bccb52b423ff72e3f9e3" src="https://github.com/user-attachments/assets/8fcfd9f9-23c9-459d-bcdd-d29ee0c45d29" />
<img width="951" height="570" alt="1fc2d9fd40f87a0c053d907b3dadc03a" src="https://github.com/user-attachments/assets/79c485c6-aec2-4027-a4a6-467a8470deda" />
<img width="1803" height="795" alt="413a43c3df8bea4d6b42d58f16a4ddec" src="https://github.com/user-attachments/assets/223122fb-8f89-4cf8-a61c-691dfba42c82" />

### Symantec:
<img width="1443" height="327" alt="597c993f9a1591b2bee00383ee184d71" src="https://github.com/user-attachments/assets/c80a9905-e167-4611-8f65-40d8b66cb44a" />
<img width="1857" height="1104" alt="56d390381df219f2f451053967f539ad" src="https://github.com/user-attachments/assets/fc659266-2408-48ca-a049-e80cb11bc21e" />

### ELK
<img width="738" height="392" alt="ce9af1a0cbaa886ced625fd05f893955" src="https://github.com/user-attachments/assets/95a117a4-acfe-4b79-b9a0-868d74879495" />
<img width="1872" height="243" alt="99f622a4f46c76e83e7c24af5f823bb4" src="https://github.com/user-attachments/assets/7c669813-d4e5-4806-8430-fac1368aea40" />
<img width="2367" height="1155" alt="6e60d4a4df4b1a9331567ba88e6ac2ac" src="https://github.com/user-attachments/assets/9a206878-92f7-45ad-a9ec-0d82fe9e0cd4" />
ELK configuration as follows
<img width="1691" height="483" alt="348a470c71728a3081e668ae4d0f0d98" src="https://github.com/user-attachments/assets/615b895e-7c04-4e83-98e6-c776e632343f" />

<img width="1155" height="7611" alt="945ced9e6b18dfafcb64da45c919d0f7" src="https://github.com/user-attachments/assets/9857adc0-a049-448f-a189-8091a2bd6789" />


## 📖 Usage Guide

### ⚠️ Strongly Recommended

Convert the generated **exe** to **Shellcode** and load/execute it with a **custom loader**.

**Why?**
As the number of tool users grows, the static signature of the `exe` may be flagged by security software. Converting to Shellcode and pairing it with your own loader can significantly improve evasion effectiveness.

**Don't worry**
The author will **refactor and release new versions weekly**, continuously updating to counter signature database upgrades.

---

## 🚀 Quick Start

### 1. Server Deployment

Launch LeekShell.exe directly
Access the console from your browser (default): `http://127.0.0.1:4433`

### 2. Standalone Listener Setup (using port 80 as an example)

Navigate to `Listeners` → fill in the port number → click `Add` to add a new listener.

### 3. Payload Generation

Fill in the server IP and listener port number, then click **Generate**.
The browser will automatically download a generated **EXE file**.

### 4. Actual Running Results

> The current version only supports command execution, with good stealth.
> (Screenshots omitted; readers may test and verify themselves)

---

## 🚀 Linux Agent

Same Server, same console, same operation logic — only the target machine changes from Windows to Linux.
<img width="2398" height="743" alt="image" src="https://github.com/user-attachments/assets/467f6884-332f-4321-b81f-f09d8b20a74b" />
<img width="2538" height="1047" alt="image" src="https://github.com/user-attachments/assets/b90d7d9d-d60d-4782-b024-38e0b4e644b8" />
<img width="2529" height="929" alt="image" src="https://github.com/user-attachments/assets/2802ac04-08b8-46a4-a9b8-48ffe8c8f790" />



## 🤔 Why Build a New C2?

### Current Pain Points

| C2 Framework | Problem |
|--------|------|
| **Cobalt Strike** | Signatures thoroughly dissected; even with stageless and sleep mask, traffic and behavior patterns still have strong signatures |
| **Sliver** | Open source but code is public; commercial EDR can build targeted detection rules |
| **Other niche C2s** | Incomplete features, poor stability, evasion relies basically on third-party loaders, lengthy operation chain |

### Core Requirements for Red Team C2

- **Stable beacon**: Works across network environments
- **Stealthy traffic**: Ports and communication protocols freely customizable
- **Evasion**: At least withstands static + dynamic detection by mainstream EDR (especially heavyweights like Kaspersky)
- **Sufficient features**: Command execution, file upload/download, process management, in-memory execution, and other basic capabilities are essential

**LeekShell is built for these goals.**

> Of course, evasion is always a cat-and-mouse game. Kaspersky not detecting it during testing doesn't mean it won't in the future. That's also why I set up a communication group — **evasion has a shelf life, and I need your feedback for continuous iteration**.

---



## ⚠️ Disclaimer

1. **Legal Use**: LeekShell is intended solely for **authorized security testing, penetration testing, red team exercises, attack-defense competitions**, and other legal scenarios. Users must ensure they have obtained **written authorization** for the target system and comply with the laws and regulations of their country and region (including but not limited to the Cybersecurity Law of the People's Republic of China and the Data Security Law).
2. **Prohibited Malicious Behavior**: It is strictly forbidden to use LeekShell for any **unauthorized intrusion, data theft, system destruction, ransomware, malicious control**, or other illegal activities. All legal liability arising from users' violation of laws and regulations or misuse of the tool **shall be borne solely by the user and is unrelated to the author**.
3. **Technical Exchange**: The content in this article and shared within the group is solely for **cybersecurity technical research and exchange**. The author does not encourage or support any form of black-market or malicious attack behavior.
4. **Tool Risks**: As a self-developed tool, LeekShell may contain unknown bugs or security flaws. Users should assess risks themselves and test in isolated environments. The author is not responsible for any direct or indirect losses caused by the use of this tool.
5. **Reserved Rights**: The author reserves the right to stop sharing, updating, or modifying LeekShell at any time. The features and evasion results described in this article are test results under specific environments and are not guaranteed to remain effective long-term in other environments.

**Please read this disclaimer carefully before downloading or using. If you do not agree, please immediately stop using and delete all related files.**

---

## 📄 License

This project is limited to learning, research, and legally authorized use. Commercial use or illegal distribution is strictly prohibited.

---

## Changelog


📅 2026.06.12
  - Added Symantec bypass strategy
  - Server side changed to out-of-the-box EXE format
  - Added program icon

📅 2026.06.16
  - Added graphical file management (view/upload/download/delete)
  - Agent added DLL generation mode (exporting Load / Start functions)


📅 2026.06.23
  - Added process management (list view/process termination)
  - Added service management (enumerate/start/stop/restart)
  - Fixed Win11 pop-up not disappearing issue

📅 June 30, 2026 Update

New:
  - Linux Agent officially launched (C++ development)
  - Supports TCP direct connection beacon
  - Supports command execution (shell)
  - Supports graphical file management (view/upload/download/delete)
  - Supports graphical process management (list view/process termination)
  - Shares the same Server and console with Windows Agent

In development:
  - Linux multi-platform beacon adaptation
  - Linux one-click backdoor deployment

Fixes:
  - Several stability optimizations

📅 July 9, 2026 Update

New:
  - LeekShell server officially supports Linux
  - One-click run: ./LeekShell
  - Covers Ubuntu / Debian / CentOS / Kali and other mainstream distributions
  - All features fully consistent with Windows version

Optimizations:
  - Cross-platform refactoring of server code
  - Removed Windows-specific dependencies
  - Out-of-the-box, no Python environment configuration needed

📅 July 22, 2026 Update

New:
  - WSS (WebSocket over TLS) encrypted communication protocol
  - Supports coexistence of WSS and TCP dual modes
  - Linux Agent simultaneously supports WSS protocol

Rewritten:
  - Windows Agent command execution module fully rewritten
  - Pipe reading efficiency improved, output speed optimized
  - Long-duration command stability optimized
  - Complete error output capture

Compatibility:
  - Linux Agent minimum supported Ubuntu 18.04
  - Covers Ubuntu 18/20/22/24, Debian 10/11/12, CentOS 7/8/9

Evasion:
  - Kaspersky Premium + EDR: ✅ Successful beacon, no alerts
  - Symantec EPP/EDR: ✅ Successful beacon, no alerts

 📅 2026.08.03

  **New:**
    - Two-layer authentication system: enterprise-style disguised login page + C2 dark login (anti-fingerprinting)
    - Dynamic listener management: real-time add/delete TCP / WSS listener ports via web interface
    - Payload generator upgrade: supports WSS EXE/DLL, Linux ELF (x86_64)
    - WSS certificate auto-generation (auto_cert), automatically issued when certificate is missing

  **Optimizations:**
    - Server single-file packaging (PyInstaller), out-of-the-box on both Windows/Linux
    - Supports three-layer configuration override: config.yaml / environment variables / CLI parameters
    - Login failure lockout mechanism, anti-brute-force

  **Fixes:**
    - Fixed WSS disconnection after long-duration commands
    - Fixed GBK→UTF-8 encoding garbled characters in command output
