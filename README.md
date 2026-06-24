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


  Keypad Row Pins    -->  Mega Digital Pins [23, 25, 27, 29]
  Keypad Column Pins -->  Mega Digital Pins [31, 33, 35, 37]

💻 Manual Developer Setup (No .EXE Compilation)
If you prefer to run the system directly from raw source code within a development environment instead of waiting for the compiled standalone executable, follow this instruction stack:

1. Clone the Space
Bash
git clone [https://github.com/dixon-team-tech/ManGOS.git](https://github.com/dixon-team-tech/ManGOS.git)
cd ManGOS
2. Configure Python Software Prerequisites
Open PowerShell or your terminal environment and pull down the requisite automation and GUI packages:

Bash
pip install customtkinter pygetwindow pyserial pyautogui requests pyinstaller
3. Flash the Core Firmware
Open the Arduino IDE.

Install the required graphics libraries via the Library Manager:

Adafruit GFX Library

Adafruit BusIO

MCUFRIEND_kbv

Keypad

Connect your Mega 2560 to your PC via its USB cable.

Select your correct Board type (Arduino Mega or Mega 2560) and COM port under the Tools menu.

Open /firmware/mangos_core.ino and hit Upload.

4. Execute the Desktop Companion App
Once the board successfully finishes flashing, close the Arduino IDE (to free up the COM connection) and spin up the Python background daemon:

Bash
python mangos_app.py
📬 Under-The-Hood Communication Protocol
The ecosystem operates via an asynchronous, lightweight serial string packet network:

The Handshake: On system startup, the desktop app launches its auto-detect thread, scanning Windows device trees for specific Vendor and Product IDs (VID/PID) linked to ATmega2560 boards, claiming the port instantly.

The Upstream Telemetry Loop: Every 10 seconds, the Python layer calls out to an external API to pull back regional meteorological states, parses local time vectors, and sends a compressed package down the pipe:

DATA_DASH:12:34 PM|Wednesday, June 24|72F Sunny\n

The Downstream Action Trap: Pressing any physical key immediately switches display arrays locally on the screen and drops an execution index out the hardware serial port:

LAUNCH_APP_IDX:3\n

The companion app intercepts this string and targets the exact payload sequence matching that index to execute system apps or macro keys via the Windows shell.

📄 License
This ecosystem is open-sourced under the terms of the MIT License. You are completely free to fork, modify, redistribute, or use ManGOS inside proprietary projects as long as the original copyright banner remains intact.

***

### Key Upgrades in this Readme:
* **Clean Code Blocks:** Wrapped your script dependencies, terminal steps, and physical wire paths into highly readable markdown fields.
* **Polished Compatibility Grid:** Consolidated your scattered compatibility tables into a single, clean overview highlighting what works and exactly what *doesn't* work.
* **Detailed Step-by-Step Build Section:** Replaced the brief `pip` block with full installati
