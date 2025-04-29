# 🕹️ IoT Relay Manager

A modern, web-based automation scheduler that remotely controls a relay module through MQTT and WebSocket communication.

## 🔍 Overview

This system allows users to schedule lighting (or other appliances) through a clean, responsive web UI. It sends commands via WebSocket and MQTT to an Arduino connected to a relay.

### 🔁 System Flow:
1. User sets ON/OFF times in the browser
2. WebSocket server checks schedule periodically
3. Commands are sent to the MQTT broker
4. A Python MQTT subscriber forwards commands to the Arduino
5. Arduino toggles the relay accordingly

## 🧩 Components

### 🖥️ Web UI
- Built with HTML, CSS, and Bootstrap
- Input form to set Turn ON/OFF times
- Communicates with WebSocket server in real-time

### 🌐 WebSocket Server (`websocket_server.py`)
- Bridges the frontend and MQTT broker
- Checks schedules every few seconds
- Publishes ON/OFF commands to MQTT topics

### 📡 MQTT Client (`subscriber.py`)
- Subscribes to the MQTT topic
- Sends commands to Arduino via serial
- Logs all activity for debugging

### 🔌 Arduino Sketch (`arduino/relay.ino`)
- Listens to serial commands
- Controls a relay on pin 7
- "LOW" = ON, "HIGH" = OFF

---

## 🧰 Requirements

### 🔧 Hardware
- Arduino board (Uno, Mega, etc.)
- Relay module (connected to pin 7)
- USB connection between Arduino and computer

### 💽 Software
- Python 3.x
- Arduino IDE
- Web browser
- Install dependencies:

```bash
pip install -r requirements.txt
