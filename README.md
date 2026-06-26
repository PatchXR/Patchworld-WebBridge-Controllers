# PatchWorld // Universal WebBridge Controller Hub

🌐 **Live Web Preview & VR Portal:** [https://patchxr.github.io/Patchworld-WebBridge-Controllers/](https://patchxr.github.io/Patchworld-WebBridge-Controllers/)

![Controller Hub UI Preview](https://img.shields.io/badge/Patchworld-VR%20WebBridge-10b981?style=for-the-badge&labelColor=0b0f19)
![Web MIDI](https://img.shields.io/badge/Web_MIDI-Supported-06b6d4?style=for-the-badge&labelColor=0b0f19)
![Gamepad API](https://img.shields.io/badge/Gamepad_API-60_FPS-a855f7?style=for-the-badge&labelColor=0b0f19)

---

## 🌟 Overview

The **PatchWorld Universal WebBridge Controller Hub** is a next-generation Single Page Application (SPA) styled as a *Cyberpunk Audio Modular Rack*. It acts as a real-time, bi-directional hardware translator between physical laboratory controllers (USB MIDI keyboards, Gamepads, DIY Microcontrollers, Arduino) and the **Patchworld VR Audio Engine**.

Whether loaded inside Meta Quest VR via a Patchworld `Browser` block (powered by Vuplex 3D WebView) or tested in a standard Desktop web browser, the Hub polls physical hardware movements and routes them instantly into Patchworld VR Wireless Jolts (`send//`).

---

## ✨ Key Features & Capabilities

### 🎹 1. Web MIDI I/O Matrix
* **Hardware Plug & Play:** Automatically discovers standard USB MIDI keyboards, drum pads, modular synths, and OS-paired Bluetooth MIDI controllers.
* **Full Protocol Routing:** Converts Note On/Off velocities, Control Change (CC) faders/knobs, and Pitch Bend wheels into customizable wireless network channels.
* **Bi-directional VR Feedback:** Subscribes to the VR wireless channel `midi_led_1`. When triggered by a virtual VR block, the Hub sends real physical MIDI Out messages to illuminate hardware LEDs on your external controller.

### 🎮 2. Universal Gamepad & VR Controller Engine
* **Universal W3C Enumeration:** Dynamically inspects hardware capabilities (`gp.axes` and `gp.buttons`). Adapts automatically whether you connect an **Xbox 360/Series Controller**, **PlayStation DualSense**, **Nintendo Switch Pro**, **Arcade Stick**, or **Meta Quest Touch Pro** VR controllers.
* **VR Anti-Lag Protection:** 
  * *Configurable Joystick Deadzone* (default `0.08`) eliminates analog drift.
  * *Delta Broadcast Threshold* (default `0.01`) prevents network spam when resting fingers on joysticks.
  * *Engine Throttling Rate Limiter* caps outgoing packets to ~40 jolts/sec per channel to preserve Unity VR frame rates.
* **Haptic Rumble Feedback:** Subscribes to the VR wireless channel `rumble`. Any trigger fired inside the virtual room instantly drives dual-motor vibration actuators (`playEffect('dual-rumble')`) on physical gamepads.

### 🔌 3. Raw Web HID & Web Serial Inspector
* **DIY Hardware Integration:** Features manual pairing portals to authorize raw USB human interface devices (HID) and Web Serial COM ports (e.g., Arduino sending telemetry at 9600 baud).

### ⌨️ 4. Virtual Keypad Matrix
* **No-Hardware VR Fallback:** A dedicated on-screen trigger pad matrix playable via mouse clicks or PC keyboard shortcuts (`Space`, `Enter`, `Q`, `W`, `E`, `R`, `1` to `4`). Perfect for testing VR room logic directly inside the Unity Editor or desktop simulations.

### 📡 5. Live Jolt Packet Inspector & Routing Cache
* **Real-time Network Console:** Monitors all outgoing (`📤 OUT SEND//`) and incoming (`📥 IN RECV//`) bridge traffic with timestamps and value inspectors.
* **Persistent Cache:** Custom channel names (e.g., changing `send//gamepad/0/axis/0` to `send//synth_filter_cutoff`) are automatically saved to browser `localStorage` and remembered across sessions.

---

## 🚀 Quick Start Guide (How to Use in VR)

1. **Launch Patchworld VR** on your Meta Quest headset or PC standalone build.
2. Spawn a **`Browser` block** in your patch.
3. Spawn a **`Web Bride`** and connect it to the Browser.
4. Set the browser URL to the live portal:  
   `https://patchxr.github.io/Patchworld-WebBridge-Controllers/`  
   *(Or point to your local development file `file:///.../index.html`).*
5. **Awaken Browser Hardware:** Click anywhere inside the browser display, then press any button or turn a knob on your physical controller.
6. **Inspect Live VU Meters:** Select your device tab on the left sidebar. Move joysticks or faders to watch the green/cyan VU bars pulse in real time.
7. **Assign Channels:** Look at the channel address column (e.g., `send//gamepad/0/axis/1`). You can rename it to anything you want.
8. **Receive in VR:** Spawn a **`Receive Jolt` block** anywhere in your VR world and type the exact matching string (e.g., `gamepad/0/axis/1`). Connect its output cable to any synthesizer frequency, light intensity, or spatial parameter!

---

## 📐 Layout & Viewport Architecture

Built specifically to conquer VR web viewports (Chromium CEF / Android System WebView):
* **Strict Viewport Locking (`height: 100%`)**: Binds document flow strictly to the rendered window bounds, preventing vertical layout shifts or clipping when browser zooming.
* **Pinned Headers & Footers (`flex-shrink: 0`)**: Top status headers, slider controls, and the bottom packet monitoring console remain permanently anchored.
* **Isolated Scrollable Lists**: When controllers possess extensive control arrays (such as 20+ gamepad buttons), *only the central control list scrolls*, keeping the navigation and diagnostic frames fixed in place.

---

*Developed for the Patchworld VR Community.*
