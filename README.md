# IoT-Based Wi-Fi Controlled RC Car with Cloud Telemetry Logging

An IoT Smart Car project featuring an ESP32 microcontroller that enables real-time driving control via a local web interface. Simultaneously, it streams vehicle telemetry—such as driving actions, battery voltage, and Wi-Fi signal strength—to the ThingSpeak cloud platform for remote monitoring and data analysis.

## Features
* **Zero-Lag Local Control:** Uses an ESP32 web server to serve a responsive, touch-friendly HTML5 steering interface.
* **IoT Cloud Monitoring:** Integrates with the **ThingSpeak API** to log vehicle analytics over the internet.
* **Live Telemetry:** Tracks real-time status including movement logs, power levels, and Wi-Fi signal metrics (RSSI).
* **Hardware Battery Safety:** Implements an analog voltage reader via a voltage divider to prevent over-discharge.

---

## Hardware Requirements
* **Microcontroller:** ESP32 (e.g., DOIT ESP32 DEVKIT V1)
* **Motor Driver:** L298N, L293D, or DRV8833 H-Bridge Module
* **Chassis:** 2WD or 4WD Robot Car Chassis with DC Motors
* **Power Source:** 7.4V / 8.4V LiPo Battery or 18650 cells

---

## Pin Configuration

### DC Motors (H-Bridge Driver)
| ESP32 GPIO Pin | Motor Driver Function | Description |
|---|---|---|
| **GPIO 12** | MOTOR_L_Fwd | Left Motor Forward |
| **GPIO 13** | MOTOR_L_Rev | Left Motor Reverse |
| **GPIO 14** | MOTOR_R_Fwd | Right Motor Forward |
| **GPIO 27** | MOTOR_R_Rev | Right Motor Reverse |

### Analog Inputs
| ESP32 GPIO Pin | Sensor Circuit | Purpose |
|---|---|---|
| **GPIO 34** | Voltage Divider Junction | Measures Battery Level (Safe 0-3.3V range) |

---

## ThingSpeak Cloud Setup

Create a channel on [ThingSpeak](https://thingspeak.com/) and assign the following fields:
* **Field 1:** `Movement Command` (Logs: 0 = Stop, 1 = Forward, 2 = Backward, 3 = Left, 4 = Right)
* **Field 2:** `Battery Voltage` (Logs actual battery voltage in Volts)
* **Field 3:** `Wi-Fi RSSI` (Logs network signal strength in dBm)

---
[Battery Positive (+)] ---- [ 10kΩ Resistor ] ----+---- [ 10kΩ Resistor ] ---- [ GND / Battery (-)]
                                                 |
                                           (To GPIO 34)
