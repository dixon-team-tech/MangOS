# ManGOS 🥭

ManGOS is a high-performance, open-source hardware macro deck and dynamic desktop companion ecosystem engineered for Windows 10 and Windows 11. Built with an optimized C++ state machine running on an ATmega2560 hardware architecture and backed by a multi-threaded Python desktop automation client, ManGOS transforms physical inputs into intelligent, context-aware desktop automations.

Featuring a gorgeous Material You-inspired UI with multi-pass 3D drop shadows, pagination carousel tracking, and automated contextual layout swapping, it brings true production-grade stream deck capabilities to custom, open-source hardware.

---

## 🚀 Target Release Date
* **Project Status:** Active Development  
* **Official Public Launch:** **July 1st** > *Check back here on July 1st to download the compiled standalone desktop application installer (`.exe`), 3D printable enclosures, and production-ready stable firmware (`.ino`).*

---

## ✨ Core Architecture Features

* **🔌 Plug-and-Play (Zero-Config Auto-Detect):** No manual COM port hunting. The Python background service scans Windows hardware controller strings natively to lock onto your board automatically, whether it uses an official USB chip or a budget CH340 interface.
* **🧠 Dynamic App Context Awareness:** ManGOS actively polls your active workspace. Switching to a code editor, web browser, or chat client fires background serial commands to the board, instantly swapping macro pages and labels on your display to match your active program.
* **🎨 Material You GUI Stack:** Ditch old, flat hobbyist interfaces. ManGOS utilizes a refined 3D card canvas featuring geometric accent bars, custom proportional typography, and live-rendering carousel pagination indicators.
* **⚡ Multi-Threaded Automation Engine:** Powered by a `customtkinter` background daemon that cleanly isolates serial pipelines, web scrapers (live weather data), and Windows API shell execution layers to eliminate terminal or screen redraw lag.

---

## 🛠️ Hardware Ecosystem Compatibility

Because the parallel display shield requires a direct, high-bandwidth physical bus routing layout, hardware component choice is critical.



<img width="362" height="552" alt="image" src="https://github.com/user-attachments/assets/5f262e19-91f4-4de6-8d2e-0e8473c5c1cb" />



### 1. Supported Microcontrollers
| Board Type | Compatibility Status | Implementation Notes |
| :--- | :--- | :--- |
| **Official Arduino Mega 2560 R3** | ✅ Fully Certified | **Recommended.** Gold standard. Uses the original ATmega16U2 chip for ultra-stable serial tracking. |
| **Elegoo Mega 2560 R3** | ✅ Fully Certified | Premium drop-in clone. Employs identical pinouts and processor layouts. |
| **IEIK / RobotDyn Mega 2560** | ✅ Fully Certified | Excellent component quality for heavy-duty desktop deployment. |
| **Generic CH340G Mega 2560** | ✅ Fully Certified | Budget-friendly clone. The Python app auto-detect script maps this chip signature natively. |
| **RobotDyn Mega 2560 PRO (Embed)**| 🔶 Supported | **Compact Build.** Shrinks the footprint entirely. Perfect for tight enclosures, but requires manual wire mapping to the display rather than standard shield mounting. |
| **Arduino Uno R3 / Nano** | ❌ Incompatible | Insufficient flash memory for proportional font stacks (32KB limit). Lacks physical I/O lanes for a parallel display bus. |
| **Arduino Due** | ❌ Incompatible | **High Danger.** Runs on 3.3V logic. Connecting a 5V parallel shield will permanently destroy the microcontroller. |
| **Raspberry Pi Pico / ESP32** | ❌ Incompatible | Mismatched hardware architectures. Requires an entirely different graphical library register ecosystem. |

### 2. Display Layer Requirements
* **Screen Specifications:** 3.5" TFT LCD Shield (8-bit or 16-bit Parallel Interface).
* **Supported Driver ICs:** ILI9486 or ST7796S chipsets.
* **Form Factor:** Standard female header shield profile engineered to press directly onto an Arduino Mega's primary and dual-row expansion I/O banks.

### 3. Keypad Matrix Map
* **Type:** 4x4 Mechanical Matrix Keypad (16 total switches).
* **Footprint:** Utilizes an 8-wire interface split cleanly into 4 Rows and 4 Columns.

---

## 📐 Hardware Wiring & Pin Mapping

If you are using a standard shield setup, press the 3.5" Screen Shield flat onto your Mega 2560 headers. Then, route your 4x4 matrix keypad directly into the remaining digital pin tracks using the map below:

```text
  Keypad Row Pins    -->  Mega Digital Pins [23, 25, 27, 29]
  Keypad Column Pins -->  Mega Digital Pins [31, 33, 35, 37]
