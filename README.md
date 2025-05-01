# 🛠️ Smart IoT-Based Pothole Detection and Filling System

A smart, low-cost solution for detecting and filling potholes using computer vision and IoT. This system integrates real-time pothole detection using an AI-powered ESP32-CAM module and an Arduino-controlled robotic unit that autonomously repairs potholes on roads.

---

## 📌 Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [System Architecture](#system-architecture)
- [Hardware Components](#hardware-components)
- [Software Stack](#software-stack)
- [Wiring & Connections](#wiring--connections)
- [How It Works](#how-it-works)
- [Getting Started](#getting-started)
- [YOLOv8 Model Integration](#yolov8-model-integration)
- [Future Improvements](#future-improvements)
- [Contributors](#contributors)
- [License](#license)

---

## 🚀 Project Overview

This project tackles the growing issue of potholes with a fully autonomous system. It uses:
- An ESP32-CAM module running a YOLOv8 model for pothole detection.
- Arduino-based robot to navigate roads, stop at potholes, and activate a mini filling mechanism.
- Real-time location logging using GPS and cloud communication.

---

## 🎯 Features

- Real-time pothole detection via AI model on ESP32-CAM
- Location tracking using GPS
- Cloud update of pothole data (optional)
- Fully automated repair using submersible pump and actuator
- Line-following robot base for navigation

---

## 🧠 System Architecture

      +-------------------+
      | ESP32-CAM + YOLOv8| ← Captures & detects potholes
      +-------------------+
               │
     GPIO/UART Connection
               ↓
    +---------------------+
    |    Arduino Uno      | ← Controls motion & pump
    +---------------------+
         │         │
         ↓         ↓
 Motors (4WD)   Submersible Pump


---

## 🔌 Hardware Components

| Component               | Quantity |
|------------------------|----------|
| ESP32-CAM Module       | 1        |
| FTDI Programmer        | 1        |
| Arduino Uno R3         | 1        |
| Ultrasonic Sensor      | 1        |
| IR Sensor (TCRT5000)   | 3–5      |
| L298N Motor Driver     | 1        |
| Submersible Pump       | 1        |
| 4WD Robot Chassis      | 1        |
| GPS Module (e.g., NEO-6M) | 1     |
| 12V Li-ion Battery     | 1        |

---

## 💻 Software Stack

- [YOLOv8](https://github.com/ultralytics/ultralytics)
- Arduino IDE (Embedded C)
- Python (for training the model)
- PlatformIO / ESP-IDF (optional)
- MicroPython (optional alternative)

---

## 🔌 Wiring & Connections

See the diagram in `/hardware/esp32-cam-ftdi-wiring-diagram.png` for how to connect ESP32-CAM with FTDI to upload code.

> **Note:** IO0 must be connected to GND while flashing the ESP32-CAM.

---

## 🧪 How It Works

1. ESP32-CAM scans the road while robot moves forward.
2. On pothole detection, ESP32 sends a signal to Arduino.
3. Arduino stops the robot, activates pump via relay, and fills the pothole.
4. Location is logged using GPS (if connected).
5. Robot resumes its path.

---

## 🧠 YOLOv8 Model Integration

The trained `best.pt` model detects potholes. Model was trained for 15+ epochs on a custom dataset.  
Converted to TensorFlow Lite/ONNX (optional) for use with ESP32-CAM + Edge ML support (basic inference via lightweight methods).

> For now, detection is simulated by image recognition results sent via GPIO to Arduino.

---

## 🛠️ Getting Started

1. Connect ESP32-CAM to FTDI programmer.
2. Upload `esp32_cam_pothole_detection.ino` using Arduino IDE.
3. Upload Arduino code to Arduino Uno.
4. Assemble robot chassis and attach components.
5. Power on and place on line-following track.

---

## 🌱 Future Improvements

- Real-time cloud sync of pothole logs via MQTT
- Use Jetson Nano or Raspberry Pi for edge processing
- Better material dispensing using solenoids and level sensors
- SMS/Alert system to maintenance teams

---

## 👨‍💻 Contributors
ion
- **Aniketh Menon** 
- **Varun Suresh** 
- **Arunachala** 

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
