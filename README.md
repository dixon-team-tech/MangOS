# ManGOS 🥭

ManGOS is a high-performance, open-source hardware macro deck and dynamic desktop companion ecosystem designed for Windows 11. Built with an optimized C++ state machine running on an Arduino Mega and a multi-threaded Python background controller, ManGOS transforms physical inputs into intelligent desktop automations.

Featuring a gorgeous Material You-inspired UI with multi-pass 3D drop shadows and automatic contextual page swapping, it brings true stream-deck capabilities to custom hardware.

---

## 🚀 Target Release Date
> **Status:** Active Development  
> **Official Public Release:** **July 1st** > *Check back here on July 1st to download the compiled standalone desktop application installer (`.exe`) and production-ready stable firmware (`.ino`).*

---

## ✨ Core Architecture Features

* **🔌 Plug-and-Play (Zero-Config Auto-Detect):** No more hunting for COM ports. The Python backend scans Windows USB controller layers natively to hook onto the Arduino Mega automatically.
* **🧠 Dynamic App Context Awareness:** ManGOS watches your active windows. Switching to a code editor, web browser, or chat program sends instant telemetry to the board, dynamically updating keys and macros on your screen.
* **🎨 Material You GUI Stack:** Upgraded from legacy hobbyist interfaces to a beautiful, clean 3D card layout featuring geometric separation lines, smooth progress bar loaders, and carousel pagination dots.
* **⚡ Multi-Threaded Engine:** Handled via a python `customtkinter` background daemon that isolates serial communications, weather parsing API requests, and Windows API shell executions to avoid interface lag.

---

## 🛠️ Hardware Ecosystem Stack

* **Microcontroller:** Arduino Mega 2560 R3
* **Display Layer:** 3.5" TFT LCD Shield (ILI9486 / MCUFRIEND_kbv wrapper)
* **Input Array:** 4x4 Mechanical Matrix Keypad
* **Font Core:** Adafruit_GFX Proportional Typography Engine

---

## 💻 Software & Library Requirements

The final desktop companion can be run as a standalone executable, but for development environments, the ecosystem leverages:

```bash
pip install customtkinter pygetwindow pyserial pyautogui requests pyinstaller
