# Arduino Health Monitoring System with Firebase Integration

A comprehensive Arduino-based health monitoring system that captures ECG, GSR, SpO₂, Heart Rate, Temperature, and Apnea detection and uploads the data to Firebase Realtime Database for remote monitoring.

---

## Table of Contents

- Features
- Hardware Requirements
- Software Requirements
- Circuit Connections
- Installation
- Configuration
- Usage
- Notes
- License

---

## Features

- Real-time acquisition of ECG, GSR, Heart Rate, SpO₂, and Temperature.
- Optional FFT analysis for ECG signal frequency detection.
- Apnea detection based on low SpO₂, BPM, or GSR readings.
- Integration with Firebase Realtime Database for cloud-based storage.
- Supports I2C and UART communication for sensors.
- Fully compatible with ESP32, Arduino UNO, ESP8266, and other boards with minor modifications.

---

## Hardware Requirements

- ESP32 / Arduino UNO / ESP8266 (recommended ESP32)
- DFRobot Blood Oxygen Sensor (MAX30102)
- ECG electrodes
- GSR sensor
- Optional: Temperature sensor (if not using MAX30102 internal)
- Jumper wires and breadboard

---

## Software Requirements

- Arduino IDE (latest version)
- Libraries:
  - DFRobot_RTU
  - DFRobot_BloodOxygen_S
  - arduinoFFT
  - FirebaseESP32
  - WiFi
  - TokenHelper and RTDBHelper from Firebase ESP32 Addons

---

## Circuit Connections

| Sensor        | Arduino/ESP32 Pin  |
|---------------|------------------|
| MAX30102 VCC  | 3.3V / 5V        |
| MAX30102 GND  | GND              |
| MAX30102 SDA  | SDA (I2C)        |
| MAX30102 SCL  | SCL (I2C)        |
| ECG DATA      | 36 (ESP32 ADC)   |
| ECG LOD+      | 19               |
| ECG LOD-      | 18               |
| GSR           | 39               |

*Note: Use SoftwareSerial on boards without multiple hardware UARTs.*

---

## Installation

1. Clone or download this repository.
2. Open the Arduino IDE and install all required libraries.
3. Open `main.ino` and ensure proper board selection:
   - Tools → Board → ESP32 Dev Module / Arduino UNO / ESP8266
4. Connect your hardware as per the circuit diagram above.

---

## Configuration

Edit the following sections in the code before uploading:

```cpp
#define WIFI_SSID "YourSSID"
#define WIFI_PASSWORD "YourPassword"
#define API_KEY "YourFirebaseAPIKey"
#define USER_EMAIL "YourEmail"
#define USER_PASSWORD "YourPassword"
#define DATABASE_URL "YourFirebaseDatabaseURL"
```

Optional sensor selection:

```cpp
#define ECG_USE     // Enable ECG
#define GSR_USE     // Enable GSR
#define FFT_USE     // Enable FFT on ECG
```

---

## Usage

1. Power the board and open the Serial Monitor at 115200 baud.
2. The system will connect to Wi-Fi and Firebase, then start reading sensor data.
3. Readings are displayed in Serial Monitor and uploaded to Firebase every 5 seconds.
4. Apnea alerts trigger automatically based on sensor thresholds.

---

## Notes

- Ensure Firebase Authentication and Realtime Database rules allow your device to write.
- Adjust the sampling rate for FFT if needed (`samplingFrequency`).
- ECG and FFT require careful electrode placement for accurate readings.
- GSR values may need calibration depending on the user.

---
