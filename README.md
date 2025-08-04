# IoT-Enabled Smart Medibox

This repository details the "Smart Medibox," a project developed as part of the **EN2853 - Embedded Systems and Applications** module. The primary goal of this device is to assist users in managing their medication schedules and ensuring their medicines are stored in optimal environmental conditions.

The project was developed in two distinct parts:
1.  **Part 1: Core Functionality Simulation:** The initial development focused on creating a fully-functional simulation of the Medibox on the Wokwi platform. This version implemented essential features such as timekeeping, medication alarms, and on-device environmental monitoring.
2.  **Part 2: Advanced IoT Enhancement:** The second part expanded on the initial design by integrating advanced IoT capabilities. This involved connecting the Medibox to a Node-RED dashboard for remote monitoring and control, and implementing an automated system to protect light-sensitive medicines.

## Features

### Intelligent Medication Reminders
*   **Customizable Alarms**: Users can set, view, and delete multiple alarms to receive timely reminders for their medication.
*   **Time Zone Synchronization**: The device automatically fetches the current time from an NTP server and can be configured with a UTC offset to display the correct local time.
*   **Multi-Alert System**: When it's time to take medicine, the Medibox provides clear alerts using a combination of a buzzer, an LED indicator, and a message on the OLED display.
*   **Snooze Functionality**: An integrated push-button allows users to either stop the alarm or snooze it for five minutes.

### Advanced Environmental Control
*   **Temperature & Humidity Monitoring**: An internal DHT sensor constantly monitors the temperature and humidity inside the storage compartment. The device issues warnings if conditions exceed predefined healthy limits (Temperature: 24°C-32°C, Humidity: 65%-80%).
*   **Light-Sensitive Protection**: A Light Dependent Resistor (LDR) measures ambient light intensity to protect light-sensitive medications.
*   **Automated Shading System**: A servo motor controls a physical shaded window, dynamically adjusting its position to regulate the amount of light entering the box. The motor's angle is calculated based on light intensity and temperature to maintain optimal storage conditions.

### Remote Management via IoT Dashboard
*   **Real-time Data Visualization**: A Node-RED dashboard provides a user-friendly interface to monitor the Medibox's environment. It features a gauge and a historical chart to visualize live and past light intensity readings.
*   **Remote Configuration**: Users can remotely fine-tune the system's behavior directly from the dashboard. This includes adjusting:
    *   The sampling and data sending intervals for the light sensor.
    *   The parameters for the automated shading system, such as the window's minimum angle, a controlling factor, and the ideal storage temperature.

## System Architecture

The core of the system is an ESP32 microcontroller, which interfaces with all sensors and actuators. For IoT functionality, the ESP32 communicates with a Node-RED dashboard using the MQTT protocol. This project uses the **HiveMQ public MQTT broker** to facilitate the communication between the device and the dashboard.

The ESP32 publishes sensor data (light, temperature) to specific MQTT topics. Simultaneously, it subscribes to configuration topics, allowing it to receive and apply settings adjusted by the user on the Node-RED dashboard in real-time.

**High-Level Architecture:**

`[ESP32 with Sensors/Actuators] <--> [HiveMQ MQTT Broker] <--> [Node-RED Dashboard]`

## Technology Stack

### Hardware
*   **Microcontroller**: ESP32
*   **Sensors**:
    *   DHT11 Temperature and Humidity Sensor
    *   Light Dependent Resistor (LDR)
*   **Actuators**:
    *   Buzzer
    *   LED
    *   Servo Motor
*   **Display**: SSD1306 OLED Display
*   **Input**: Push Button

### Software & Platforms
*   **Embedded Programming**: Arduino C/C++
*   **Simulation**: Wokwi
*   **IoT Communication**: MQTT
*   **MQTT Broker**: HiveMQ
*   **Dashboard & Backend Logic**: Node-RED
