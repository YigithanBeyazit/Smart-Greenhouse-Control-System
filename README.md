# 🌿 Smart Greenhouse Control System (Z80/DMC8)

This project is an autonomous greenhouse monitoring and irrigation system developed using two synchronized Z80-based microprocessors (DMC8).

## 🚀 Project Overview
The system measures soil moisture levels and makes autonomous decisions to maintain plant health. It features a hardware-synchronized communication protocol and a dual-status monitoring interface.

### ✨ Key Features
* **Inter-Processor Communication:** Hardware-synchronized Handshake (Strobe/Busy) protocol.
* **Autonomous Irrigation:** Automatic pump control based on a predefined threshold (**30h**).
* **Dual-LED Feedback:** Visual indicators for **Critical** (Red) and **Optimal** (Green) states.
* **Real-time Monitoring:** Integrated 7-segment and Hexadecimal displays for data observation.

## 🛠 Hardware Configuration
The circuit is designed in the **Deeds** environment using **DMC8 Basic System** components.

| Component | Port | Function |
| :--- | :--- | :--- |
| **TX OB Port** | 01h | Data Bus Output |
| **TX OA Port** | 00h | Control (Strobe) Output |
| **RX IB Port** | 01h | Data Bus Input |
| **RX OB Port** | 01h | Control (Busy) Output |
| **RX OC Port** | 02h | LED/Pump Control |

## 💻 Software Implementation
The project consists of two core Assembly files:

1.  **`TX.mc8`**: Handles data generation and strobe signal timing (approx. 0.5 ms).
2.  **`RX.mc8`**: Handles strobe polling, data acquisition, and threshold-based decision making.

### 🧠 Irrigation Logic
```assembly
; Threshold: 30h (Decimal 48)
LD      A, D        ; Load humidity data
CP      30h         ; Compare with threshold
JP      C, PUMP_ON  ; If Humidity < 30h, activate Red LED
