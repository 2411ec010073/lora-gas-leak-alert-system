# 🚨 Emergency Alert System Using LoRa Module and Gas Sensor

An embedded safety system that detects hazardous gas leakage at an early stage and
transmits an emergency alert over long distances using LoRa communication —
without depending on Wi-Fi, GSM, or internet connectivity.

**Department of Electronics and Communication Engineering (ECE)**
Malla Reddy University, Hyderabad

---

## 📌 Overview

Gas leakage in industries, LPG storage facilities, factories, laboratories, and
warehouses can lead to fire, explosions, and health hazards if not detected early.
This project uses an **MQ-2 gas sensor** to continuously monitor combustible gases
and smoke, an **ESP32 microcontroller** to process readings against a safety
threshold, and **LoRa (SX1278/RA-02)** modules to wirelessly alert a remote
monitoring station.

When gas concentration exceeds the threshold:
- **Transmitter side:** LED + buzzer activate, OLED displays the gas status, and an
  emergency packet is sent via LoRa.
- **Receiver side:** The alert is received, the buzzer sounds, and the OLED
  displays **"GAS LEAKAGE DETECTED"**.

---

## 🧩 System Architecture
┌───────────────────── TRANSMITTER UNIT (Sensor Side) ─────────────────────┐
│ │
│ MQ-2 Gas Sensor ──► ESP32 ──► LED (visual alert) │
│ │ ├──► Buzzer (audible alert) │
│ │ ├──► OLED Display (gas level & status) │
│ │ └──► LoRa Transmitter ──► ~~~~ LoRa ~~~~► │
└──────────────────────────────────────────────────────────────────────────┘
│
┌───────────────────── RECEIVER UNIT (Monitoring Side) ──────▼─────────────┐
│ │
│ LoRa Receiver ──► Microcontroller ──► Emergency Alert / Monitoring │
│ / Display Unit (User / Control Room) │
└──────────────────────────────────────────────────────────────────────────┘


**Working flow:**
`Gas Detection → Sensor Reading → ESP32 Processing → Threshold Check →
Local Alarm → LoRa Transmission → LoRa Reception → Emergency Alert`

---

## ✨ Features

- Continuous real-time gas & smoke monitoring with MQ-2
- Automatic threshold-based hazard detection
- Long-range, low-power LoRa wireless alerting (~433/866 MHz)
- Local audio-visual warning (LED + buzzer + OLED) at the sensor node
- Remote monitoring station with display and buzzer
- No internet/cloud dependency — works in isolated hazardous zones
- Modular, low-cost, and scalable design

---

## 🛠️ Hardware Requirements

| Component | Purpose |
|---|---|
| ESP32 (Heltec WiFi LoRa 32 V3) | Main processing & control unit (×2) |
| MQ-2 Gas Sensor | Detects LPG, smoke, methane, propane, H₂ |
| LoRa SX1278 / RA-02 Module | Long-range wireless TX/RX |
| OLED Display (SSD1306, I²C) | Gas level & system status |
| Buzzer | Audible emergency warning |
| LED | Visual emergency indication |
| LoRa Antenna (433/866 MHz) | RF signal TX/RX |
| Regulated Power Supply | Powers all components |
| Jumper Wires / Breadboard / PCB | Prototyping & connections |
| Resistors & supporting components | Safe interfacing |

---

## 💻 Software Requirements

- **Arduino IDE** — programming & uploading
- **Embedded C/C++** — system control logic
- **ESP32 Board Package** — ESP32 support in Arduino IDE
- **LoRa Library** (e.g., `sandeepmistry/arduino-LoRa`) — LoRa TX/RX
- **Adafruit GFX + SSD1306 Libraries** — OLED graphics/text
- **Serial Monitor** — debugging & sensor/comm monitoring

---

## 🔌 Communication Protocols

| Protocol | Used Between |
|---|---|
| **SPI** | ESP32 ↔ LoRa SX1278 (MOSI, MISO, SCK, CS, RST, DIO0) |
| **I²C** | ESP32 ↔ OLED (SDA, SCL) |
| **ADC** | MQ-2 analog output → ESP32 ADC pin |
| **GPIO** | ESP32 → LED & buzzer control |

---

## 📁 Repository Structure
lora-gas-leak-alert-system/
│
├── README.md
├── docs/
│ ├── Project_Report.pdf
│ ├── Architecture_Diagram.png
│ ├── Circuit_Diagram.png
│ └── UseCase_Sequence_Activity_Diagrams/
│
├── transmitter/
│ └── transmitter.ino # ESP32 + MQ-2 + LoRa TX + OLED + buzzer/LED
│
├── receiver/
│ └── receiver.ino # ESP32 + LoRa RX + OLED + buzzer
│
├── hardware/
│ ├── circuit_diagram.png
│ └── component_list.md
│
└── results/
├── experimental_setup.jpg
├── serial_monitor_output.png
└── performance_analysis.md

🔮 Future Scope

Multiple gas sensors (LPG, CH₄, CO, combustible gases)

Sensor calibration, temperature compensation & drift correction

IoT/cloud dashboard + mobile app notifications

GPS-based leak location identification

AI/ML-based anomaly detection & false-alarm reduction

Automatic ventilation, exhaust fan, and emergency power cutoff

Solar power + battery backup

Multi-node LoRa network with centralized gateway monitoring

Antenna & LoRa parameter optimization for extended range

👥 Team

Name	Roll No.
G. Srujith Reddy	2411EC010073
K. Manorahul	2411EC010106
K. Bhanuprakash Reddy	2411EC010120
M. Shivagopi	2411EC010122


Guide: Dr. Ome Nerella, Assistant Professor, Dept. of ECE

📚 References


Hanwei Electronics — MQ-2 Semiconductor Sensor Datasheet

Espressif Systems — ESP32 Technical Reference Manual

Semtech — SX1276/77/78/79 Transceiver Datasheet

LoRa Alliance — LoRaWAN Specification

Arduino IDE Documentation

Seeed Studio — Grove Gas Sensor (MQ-2) Documentation

Espressif Systems — ESP-IDF Programming Guide
