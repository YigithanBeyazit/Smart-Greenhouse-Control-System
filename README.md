# Smart-Greenhouse-Control-System
Smart greenhouse control system with DMC8 microprocessor
Smart Greenhouse Control System (Z80/DMC8)
This project is a microprocessor-based autonomous greenhouse monitoring and irrigation system developed for the Microprocessor Systems course final. It utilizes two synchronized Z80-based microprocessors to simulate real-time soil moisture management.
Project Overview:
The system measures simulated soil moisture levels and makes autonomous decisions to maintain optimal plant health. It features a robust communication protocol and a dual-status monitoring interface.
Key Features:
Inter-Processor Communication: Hardware-synchronized Handshake (Strobe/Busy) protocol.
Autonomous Irrigation: Automatic pump control based on a predefined threshold (30h).
Dual-LED Feedback: Visual indicators for "Critical" (Red) and "Optimal" (Green) moisture states.
Real-time Monitoring: Integrated 7-segment and Hexadecimal displays for data bus observation
Hardware Configuration:
The circuit is designed in the Deeds (Digital Electronics Education and Design Suite) environment using DMC8 (Basic/Enhanced System) components.
COMPONENT--------------- PORT----------FUNCTION
Transmitter(TX)OB--------01h---------Data Bus Output
Transmitter(TX)OA--------00h---------Control (Strobe) Output    
Reciever(RX)IB------------01h---------Data Bus Input
Reciever(RX)OB------------01h---------Control (Busy) Output
Receiver(RX)OC------------02h---------LED/Pump Control
Software Implementation:
SMART GREENHOUSE CONTROL SYSTEM TX.mc8: Handles data generation (incrementing humidity) and the strobe signal timing (approx. 0.5 ms).
SMART GREENHOUSE CONTROL SYSTEM RX.mc8: Handles polling of the strobe line, data acquisition, and threshold-based decision making
Irrigation Logic:
; Threshold: 30h (Decimal 48)
LD      A, D        ; Load humidity from register D
CP      30h         ; Compare with threshold
JP      C, PUMP_ON  ; If Humidity < 30h, start pump (Red LED)
