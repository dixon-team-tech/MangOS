# MangOS 🥭
MangOS is a high-performance, open-source hardware macro deck and dynamic desktop companion ecosystem engineered for Windows 10 and Windows 11. Built with an optimized C++ state machine running on an ATmega2560 hardware architecture and backed by a multi-threaded Python desktop automation client, MangOS transforms physical inputs into intelligent, context-aware desktop automations.
Featuring a gorgeous Material You-inspired UI with multi-pass 3D drop shadows, pagination carousel tracking, and automated contextual layout swapping, it brings true production-grade stream deck capabilities to custom, open-source hardware.
---
## 🚀 Target Release Date
* **Project Status:** Active Development  
* **Official Public Launch:** **July 1st** > *Check back here on July 1st to download the compiled standalone desktop application installer (`.exe`), 3D printable enclosures, and production-ready stable firmware (`.ino`).*
---
## ✨ Core Architecture Features
* **🔌 Plug-and-Play (Zero-Config Auto-Detect):** No manual COM port hunting. The Python background service scans Windows hardware controller strings natively to lock onto your board automatically, whether it uses an official USB chip or a budget CH340 interface.
* **🧠 Dynamic App Context Awareness:** MangOS actively polls your active workspace. Switching to a code editor, web browser, or chat client fires background serial commands to the board, instantly swapping macro pages and labels on your display to match your active program.
* **🎨 Material You GUI Stack:** Ditch old, flat hobbyist interfaces. MangOS utilizes a refined 3D card canvas featuring geometric accent bars, custom proportional typography, and live-rendering carousel pagination indicators.
* **⚡ Multi-Threaded Automation Engine:** Powered by a `customtkinter` background daemon that cleanly isolates serial pipelines, web scrapers (live weather data), and Windows API shell execution layers to eliminate terminal or screen redraw lag.
---
## 🛠️ Hardware Ecosystem Compatibility
Because the parallel display shield requires a direct, high-bandwidth physical bus routing layout, hardware component choice is critical.


<img width="362" height="552" alt="image" src="https://github.com/user-attachments/assets/5f262e19-91f4-4de6-8d2e-0e8473c5c1cb" />


### 1. Supported Microcontrollers
| Board Type | Compatibility Status | Implementation Notes |
| :--- | :--- | :--- |
| **Official Arduino Mega 2560 R3** | ✅ Fully Certified | **Recommended.** Gold standard. Uses the original ATmega16U2 chip for ultra-stable serial tracking. |
