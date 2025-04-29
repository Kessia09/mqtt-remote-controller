 🕹️ IoT Relay Manager

A modern, web-based automation scheduler that remotely controls a relay module using MQTT and WebSocket communication.

---

🔍 Overview

**IoT Relay Manager** lets users schedule appliances (like lights) through a simple, responsive web interface. The system interacts with an Arduino-based relay controller via WebSocket and MQTT for real-time automation.

---

 🔁 System Flow

1. User sets Turn ON and OFF times through the web UI.
2. The WebSocket server checks schedules regularly.
3. Commands are published to an MQTT topic.
4. A Python MQTT subscriber listens and forwards the command to the Arduino.
5. Arduino receives the command over serial and toggles the relay accordingly.

---

🧩 Components

 🖥️ Web UI

- Built with HTML, CSS, Bootstrap.
- Lets users define Turn ON/OFF times.
- Sends data to the WebSocket server in real-time.

 🌐 WebSocket Server (`websocket_server.py`)

- Acts as a bridge between the frontend and the MQTT broker.
- Periodically checks the user-defined schedule.
- Publishes ON/OFF commands to specific MQTT topics.

 📡 MQTT Client (`subscriber.py`)

- Subscribes to the MQTT topic.
- Sends ON/OFF commands to the Arduino via USB serial.
- Logs all actions for easy debugging.

🔌 Arduino Sketch (`arduino/relay.ino`)

- Listens for ON/OFF serial commands.
- Controls a relay connected to **pin 7**.
- `LOW` = ON, `HIGH` = OFF

---

🧰 Requirements

 🔧 Hardware

- Arduino board (Uno, Mega, etc.)
- Relay module (connected to pin 7)
- USB cable (to connect Arduino to PC)

 💽 Software

- Python 3.x
- Arduino IDE
- Web browser

---

⚙️ Installation & Setup
 1. Clone the Repository
git clone https://github.com/your-username/iot-relay-manager.git
cd iot-relay-manager
2. Install Python Dependencies
pip install -r requirements.txt

3. Upload Arduino Sketch
Open arduino/relay.ino in the Arduino IDE.

Select the correct board and COM port.

Upload the sketch to your Arduino.

4. Configure MQTT Broker
Use a public MQTT broker (like test.mosquitto.org) or set up a local broker (e.g., Mosquitto).

Update the MQTT topic and broker address in both websocket_server.py and subscriber.py.

5. Start Backend Services
Start the WebSocket server:


python websocket_server.py
Start the MQTT subscriber:
python subscriber.py

6. Open the Web UI
Open index.html in your browser.

Set the desired ON/OFF schedule.

Leave the tab open for live control.

📌 Notes
Relay status is dependent on system time, so ensure your computer time is correct.

This setup assumes the Arduino is connected to the same computer running the Python scripts.

WebSocket server and subscriber should run continuously for real-time control.
