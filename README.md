# 🛰️ Project AETHERLINK
### _A hybrid handheld console for Meshtastic mesh networks_

AetherLink is a **portable command and visualization console** that bridges **LoRa-based Meshtastic mesh networks** with a rich user interface.  
It combines a **RAK4631 (SX1262)** running Meshtastic firmware with an **ESP32-C3-DevKitC-02** frontend that drives multiple displays and controls.

This project explores **low-power distributed communication**, **embedded UI design**, and **mesh network introspection** in one cohesive device.

---

## 📡 Overview

AetherLink acts as a **command node** in a Meshtastic mesh, capable of:
- Viewing messages and network status in real time
- Displaying persistent logs or topology on an e-ink screen
- Interacting via touchscreen and physical buttons
- Bridging data to Wi-Fi dashboards or MQTT brokers

It’s designed to be a **field-deployable communicator** — part tactical tool, part research instrument.

---

## 🧩 Hardware Architecture

| Component | Role | Notes |
|------------|------|-------|
| **RAK4631 (SX1262)** | LoRa + BLE core (Meshtastic firmware) | Housed in **RAK19007 WisBlock base** |
| **ESP32-C3-DevKitC-02** | UI controller + Wi-Fi bridge | Communicates with RAK4631 via UART or BLE |
| **Waveshare 1.28" Touch LCD** | Interactive menu, live stats | SPI interface |
| **Akwox 4-button panel** | Navigation / quick actions | GPIO inputs with pull-ups |
| **2.9" E-Ink FeatherWing** | Persistent message log / topology | SPI interface |
| **MAX7219 Dot Matrix Modules** | Scrolling status / alerts | Daisy-chained SPI |
| **LiPo battery** | Power source | Charged via RAK19007 onboard circuit |
| **915 MHz antenna** | Long-range LoRa connectivity | SMA connector on RAK4631 |

---

## 🧠 System Design

[User Interface Frontend]          [Mesh Core Backend]
┌────────────────────────┐         ┌────────────────────────┐
│  ESP32-C3-DevKitC-02   │  UART   │   RAK4631 (SX1262)     │
│                        │ <──────▶│   running Meshtastic   │
│ Waveshare 1.28” LCD    │         │   BLE + LoRa mesh      │
│ Akwox Button Panel     │         └────────────────────────┘
│ MAX7219 Matrix          │
│ 2.9” E-Ink FeatherWing  │
└────────────────────────┘
        │
        └── Wi-Fi → Optional MQTT / Web Dashboard


The ESP32-C3 parses Meshtastic serial messages, renders visual data, and exposes optional network telemetry via Wi-Fi.

---

## 🚀 Planned Features

| Phase | Goal | Description |
|-------|------|-------------|
| **1** | Mesh Core Link | UART/BLE bridge to RAK4631; display node list and messages |
| **2** | UI System | Menu navigation, live metrics, message viewer |
| **3** | E-Ink Visualization | Persistent log + mesh topology render |
| **4** | MQTT Bridge | Publish node data to a web dashboard |
| **5** | Expansion | GPS, environmental sensors, OTA updates |

---

## 🔌 Example Pin Mapping (ESP32-C3)

| Peripheral | Function | GPIO |
|-------------|-----------|------|
| LCD SPI | MOSI / SCK / CS / DC | 7 / 4 / 10 / 5 |
| E-Ink SPI | Shared bus | 7 / 4 / 9 / 8 |
| Buttons | UP / DOWN / LEFT / RIGHT | 1 / 2 / 3 / 6 |
| MAX7219 | DIN / CLK / CS | 7 / 4 / 11 |
| UART to RAK4631 | TX / RX | 20 / 21 |

> _Exact mapping will be refined as hardware integration progresses._

---

## 🧰 Development Environment

- **Firmware**
  - `ESP-IDF` or `Arduino-ESP32` for the UI controller  
  - `Meshtastic` pre-built binary for RAK4631 (SX1262)
- **UI Frameworks**
  - [`LVGL`](https://lvgl.io) for the touch LCD  
  - [`GxEPD2`](https://github.com/ZinggJM/GxEPD2) for e-ink displays  
  - [`Adafruit-GFX`](https://github.com/adafruit/Adafruit-GFX-Library) for MAX7219 text rendering
- **Communication**
  - UART serial protocol between ESP32-C3 ↔ RAK4631
  - BLE (optional)
  - MQTT / WebSocket telemetry bridge (optional)

---

## 📷 Concept Preview (planned)
> *Visual mockup coming soon — handheld communicator with dual displays and SMA antenna.*

---

## 🧭 Roadmap

- [ ] Bring up RAK4631 Meshtastic firmware  
- [ ] Establish serial link and message parsing on ESP32-C3  
- [ ] Render live data on LCD  
- [ ] Add 4-button interaction system  
- [ ] Integrate e-ink logging  
- [ ] Design 3D-printed enclosure  

---

## 🛠️ Contributing

Contributions and ideas are welcome!  
If you have display driver improvements, alternate UI concepts, or mesh analytics tools, open a PR or discussion.

---

## 📜 License

MIT License © 2025 James A. Covert

---

### 🔗 References
- [Meshtastic Project](https://meshtastic.org)
- [RAKwireless WisBlock](https://store.rakwireless.com/)
- [ESP32-C3 DevKitC-02](https://www.espressif.com/)

