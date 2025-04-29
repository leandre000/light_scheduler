💡 IoT Light Scheduler Dashboard
A simple yet powerful IoT Light Scheduler that allows you to control a light or relay based on scheduled times via a user-friendly web interface.

Supports:

✅ Real Arduino hardware

🧪 Simulated Arduino (no physical hardware required)

📁 Project Structure

File	Description
light-scheduler.py	Main MQTT subscriber and serial writer for Arduino
web-socket.py	WebSocket server that forwards schedules to MQTT
fake-simulation.py	Simulated Arduino using virtual serial (loop://)
frontend.html	Web-based UI to set ON/OFF light schedules
⚙️ Requirements
🐍 Python 3.7+

📦 Install dependencies:


pip install paho-mqtt pyserial websockets
🛰️ MQTT Broker
This project uses a public MQTT broker:
IP: 157.173.101.159
Port: 1883

🚀 How to Run
🧪 Without Hardware (Simulation Mode)
Start the Fake Arduino Simulation:

Start the Light Scheduler:
python light-scheduler.py
Start the WebSocket Server:
python web-socket.py
Open frontend.html in your browser and schedule your ON/OFF times.

🔌 With Real Arduino Hardware
Edit Serial Port in light-scheduler.py:

🔄 How It Works

Step	Action
1️⃣	UI sends schedule (e.g., 10:30 ON) via WebSocket
2️⃣	WebSocket server forwards the message to MQTT
3️⃣	light-scheduler.py receives and tracks the schedule
4️⃣	At the exact time, it sends the ON/OFF command to Arduino
5️⃣	Arduino toggles the relay/light accordingly
📝 Notes
🌀 loop:// is used for virtual serial simulation (no Arduino required)

🔁 Schedules automatically reset daily at 00:00

🧠 Don't forget to import serial.urlhandler.protocol_loop for simulation to work

👤 Contact
Made with ❤️ by Izere Shema Leandre
📧 Email: iamshemaleandre@gmail.com

