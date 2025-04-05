# **Documentation for Smart Paper Feeding and Printing System**

## **1. Introduction**
This document provides a detailed explanation of the electronic system designed for a smart paper feeding and printing system. The system integrates a **Raspberry Pi 4**, an **N20 motor with an encoder**, an **optical sensor (TCRT5000)**, an **LCD display**, and a **motor driver (TB6612FNG)**. The project involves sensing paper availability, controlling the motor for feeding pages based on user input, and communicating with a printer to execute print jobs.

## **2. System Overview**
The system works as follows:
1. The **Raspberry Pi 4** acts as the main controller, handling motor control, encoder feedback, sensor input, and communication with the printer.
2. The **TCRT5000 infrared sensor** detects whether paper is available in the feeder.
3. The **N20 motor**, controlled by the **TB6612FNG motor driver**, moves the paper into the printer.
4. The **encoder attached to the N20 motor** provides feedback to measure the exact movement and count pages accurately.
5. An **LCD display** provides real-time information about the system status.
6. The **power supply module** converts AC to a regulated 5V DC supply for the Raspberry Pi and associated components.

## **3. Components and Connections**

### **3.1 Power Supply Circuit**
- A **12V to 5V regulator circuit** is implemented using an **LM7805 voltage regulator**.
- **Bridge rectifier (D5)** converts AC voltage to DC voltage.
- Capacitors (C1 = 100uF, C2 = 10uF) help in smoothing the output voltage.

### **3.2 Raspberry Pi 4 (Main Controller)**
- The **Raspberry Pi 4 (J3)** receives input signals from the **optical sensor (TCRT5000)** and the **motor encoder**.
- It controls the **motor driver (TB6612FNG)** to drive the N20 motor.
- The Raspberry Pi also manages the **LCD display** to provide user feedback.
- It communicates with the **printer** via USB or a network connection.

### **3.3 N20 Motor with Encoder**
- The motor terminals are connected to the **motor driver (TB6612FNG)** at AO1 and AO2.
- The **encoder A output** is connected to **GPIO17** of the Raspberry Pi for real-time feedback on motor movement.
- The encoder allows precise control of paper feeding length.

### **3.4 Motor Driver (TB6612FNG)**
- **AIN1, AIN2, and PWM A** from the Raspberry Pi control the motor direction and speed.
- The **STBY pin** is connected to **3.3V** to enable the driver.
- **AO1 and AO2** are connected to the **N20 motor terminals**.
- The driver is powered by a **12V source**.

### **3.5 Optical Sensor (TCRT5000)**
- The **infrared LED (A pin)** is connected to **3.3V via a 330Ω resistor (R1)**.
- The **phototransistor output (C pin)** is connected to **GPIO24** of the Raspberry Pi with a **10kΩ pull-down resistor (R2)**.
- The sensor detects the presence of paper and sends a signal to the Raspberry Pi.

### **3.6 LCD Display (LM016L)**
- The LCD display is connected to multiple GPIO pins of the Raspberry Pi.
- It provides real-time updates such as "Paper Available", "Feeding Paper", and "Printing..." messages.

## **4. Implementation**
1. **Powering Up**
   - The system is powered using a **12V DC supply**, which is stepped down to **5V** using an LM7805 voltage regulator.
   - The Raspberry Pi, motor driver, and sensor circuits are powered from the **5V** supply.

2. **Paper Detection**
   - The **TCRT5000 sensor** detects whether a paper sheet is present.
   - If no paper is detected, the system will wait and notify the user via the **LCD display**.

3. **Motor Control and Page Feeding**
   - The **Raspberry Pi** receives the print request from the server.
   - It calculates the required motor movement based on **encoder feedback**.
   - The **motor driver (TB6612FNG)** drives the **N20 motor** to push the correct number of pages into the printer.
   - Encoder feedback ensures precise control, preventing multiple pages from being pushed.

4. **Printing Process**
   - Once the required pages are fed, the Raspberry Pi sends the print job to the **printer via USB**.
   - The **CUPS (Common Unix Printing System)** manages the print operation.
   - The LCD displays "Printing..." while the job is in progress.

## **5. Conclusion**
This system enables automated, controlled paper feeding for a printer using a Raspberry Pi, an N20 motor with an encoder, and an IR sensor. The design ensures accurate page feeding by integrating motor feedback and paper detection, providing a reliable solution for smart printing applications.

---


