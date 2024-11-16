This project implements a **smart irrigation system** using **ESP32 microcontrollers** to measure soil moisture, temperature, and rain detection data in real-time. The system sends data to a Firebase Realtime Database and adjusts water output based on predefined crop categories and moisture levels, ensuring efficient and automated irrigation. This README provides details on how to replicate the project, hardware/software requirements, setup instructions, and usage.

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Hardware Requirements](#hardware-requirements)
- [Software Requirements](#software-requirements)
- [Wiring and Configuration](#wiring-and-configuration)
- [Setup Instructions](#setup-instructions)
- [Usage](#usage)
- [Future Improvements](#future-improvements)
- [Contributing](#contributing)

## Overview

This smart irrigation system measures various environmental factors to automate watering based on soil moisture, temperature, rain detection, and crop water needs. Data is sent to Firebase in real-time, allowing for data monitoring and control of irrigation motors.

### Architecture

This project involves two ESP32 microcontrollers:
1. **Sensor Node**: Collects sensor data (temperature, soil moisture, rain) and uploads it to Firebase.
2. **Motor Control Node**: Reads data from Firebase, determines water requirements, and adjusts the motor speed accordingly.

## Features

- **Automated Irrigation**: Adapts motor speed based on soil moisture, temperature, rain detection, and crop category.
- **Firebase Integration**: Utilizes Firebase Realtime Database to store and retrieve sensor data.
- **Adjustable Watering**: Different water requirements based on crop types.
- **Weather-Adaptive**: Halts irrigation if rain is detected.

 ![webpage](https://github.com/user-attachments/assets/a6141059-d511-4117-a119-c4758f422f0c)

 ![Mobile_App](https://github.com/user-attachments/assets/a2e7b69a-6299-4ef4-b086-85409c765085)



## Hardware Requirements

- **ESP32 microcontrollers** (2x)
- **DHT11 Temperature and Humidity Sensor** (for ambient temperature)
- **Soil Moisture Sensor** (Analog)
- **Rain Sensor** (Analog)
- **Motor Driver Module** (e.g., L298N)
- **12V DC Motor** for irrigation
- **Connecting Wires**
- **Power Supply** (e.g., 3.7V LiPo battery or equivalent)

## Software Requirements

- **Arduino IDE** (v1.8.13 or later) with ESP32 board support
- **Firebase ESP Client Library** for Arduino
- **DHT Sensor Library** for DHT11 sensor
- **Firebase Credentials** (API key, Database URL)

### Libraries

Install these libraries in Arduino IDE:
- [Firebase ESP Client Library](https://github.com/mobizt/Firebase-ESP32)
- [DHT Sensor Library](https://github.com/adafruit/DHT-sensor-library)

## Wiring and Configuration

### Sensor Node Connections

| Component         | ESP32 Pin |
|-------------------|-----------|
| DHT11 Data        | GPIO 4    |
| Soil Moisture     | GPIO 35   |
| Rain Sensor       | GPIO 34   |

### Motor Control Node Connections

| Component          | ESP32 Pin |
|--------------------|-----------|
| Motor Driver IN1   | GPIO 27   |
| Motor Driver IN2   | GPIO 26   |
| Motor Driver ENA   | GPIO 14   |

### Firebase Configuration

1. **API Key**: Set your Firebase API key in the code.
2. **Database URL**: Define the URL of your Firebase Realtime Database.

## Setup Instructions

1. **Set Up Firebase Project**:
   - Go to [Firebase Console](https://console.firebase.google.com/), create a project, and enable Realtime Database.
   - In the Database Rules, set permissions to allow read/write for testing (`true`) or configure securely for deployment.

2. **Configure Arduino IDE**:
   - Install the ESP32 board support via Arduino’s Board Manager.
   - Add the required libraries for Firebase and DHT11 sensors.

3. **Upload Code**:
   - Open the two separate code files provided in this project.
   - Customize Wi-Fi credentials, Firebase API Key, and Database URL in both files.
   - Upload the **Sensor Node Code** to the first ESP32.
   - Upload the **Motor Control Node Code** to the second ESP32.

## Usage

1. **Power on** both ESP32 modules.
2. **Monitor the Serial Output** for data sent and received to/from Firebase.
   - The Sensor Node reads environmental data and uploads it to Firebase.
   - The Motor Control Node reads data from Firebase and adjusts the motor speed based on conditions.

### How it Works

- **Sensor Node**:
   - Reads **temperature** from the DHT11 sensor, **moisture level** from the soil sensor, and **rain status**.
   - Sends data to Firebase every 10 seconds.
   
- **Motor Control Node**:
   - Reads **crop category** and **sensor data** from Firebase.
   - Adjusts motor speed based on soil moisture level and crop water requirements:
     - **Low Moisture**: Highest speed
     - **Medium Moisture**: Moderate speed
     - **High Moisture** or **Rain Detected**: Stops motor
   - The motor runs for 10 seconds in each cycle, then pauses for stability.

## Crop Category and Water Requirements

- **Crop Categories** (customizable in Firebase):
  - **Category 1**: Low water requirement
  - **Category 2**: Medium water requirement
  - **Category 3**: High water requirement

Adjust motor speeds within the code based on crop needs and environmental conditions.

## Future Improvements

- **Add Mobile App Interface**: Integrate a mobile app for remote monitoring and control.
- **Weather Forecasting**: Use online weather API data to adjust watering schedules.
- **Battery Optimization**: Explore power-efficient modes for longer battery life.
- **Enhanced Security**: Implement authentication and secure database rules for production.

## Contributing

Contributions to improve this project are welcome! Feel free to open issues for bug fixes or feature requests, or submit pull requests to add functionalities.

### To Contribute:
1. Fork the repository.
2. Clone the forked repository.
3. Create a new branch for your feature or fix.
4. Make changes and test thoroughly.
5. Submit a pull request detailing your changes.
