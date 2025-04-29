# 🌟 IoT Light Scheduler Dashboard

A simple IoT Light Scheduler 🕰️ that allows you to control your light or relay 💡 based on scheduled times through a web interface 🌐.

---

## ✨ Features

- ✅ Control **real Arduino hardware**.
- ✅ Run **fake Arduino simulation** (no hardware required).
- ✅ **Browser UI** to easily schedule ON/OFF times.
- ✅ **MQTT-based** communication for real-time updates.

---

## 📁 Project Structure

| File | Purpose |
|:----:|:-------|
| `light-scheduler.py` | Main MQTT subscriber and serial writer for Arduino |
| `web-socket.py` | WebSocket server forwarding schedules to MQTT |
| `fake-simulation.py` | Simulated Arduino via virtual serial (`loop://`) |
| `frontend.html` | Browser UI for setting light ON/OFF schedules |

---

## ⚙️ Requirements

- Python 3.7+ 🐍
- MQTT Broker (Public Broker IP: **157.173.101.159**, Port: **1883**)

Install dependencies:

```bash
pip install paho-mqtt pyserial websockets
```

---

## 🚀 How to Run

### 🖥️ Without Real Hardware (Simulation Mode)

1. Start the fake Arduino simulation:

    ```bash
    python fake-simulation.py
    ```

2. Start the light scheduler:

    ```bash
    python light-scheduler.py
    ```

3. Start the WebSocket server:

    ```bash
    python web-socket.py
    ```

4. Open `frontend.html` in your browser and set your ON/OFF times! 🎯

---

### 🔌 With Real Arduino Hardware

1. Change the serial port inside `light-scheduler.py`:

    Replace:

    ```python
    arduino = serial.serial_for_url('loop://', baudrate=9600, timeout=1)
    ```

    With your device port (e.g., `COM5` on Windows or `/dev/ttyUSB0` on Linux):

    ```python
    arduino = serial.Serial('COM5', baudrate=9600, timeout=1)
    ```

2. Flash your Arduino with the provided `sched_on_off.ino` sketch:

    ```cpp
    int relayPin = 2;

    void setup() {
      Serial.begin(9600);
      pinMode(relayPin, OUTPUT);
      digitalWrite(relayPin, HIGH); // Relay OFF initially
    }

    void loop() {
      if (Serial.available() > 0) {
        String cmd = Serial.readStringUntil('\n');
        cmd.trim();
        if (cmd == "ON") {
          digitalWrite(relayPin, LOW); // Relay ON
        } else if (cmd == "OFF") {
          digitalWrite(relayPin, HIGH); // Relay OFF
        }
      }
    }
    ```

3. Run:

    - `light-scheduler.py`
    - `web-socket.py`
    - Open `frontend.html`

4. ✅ Now, your real relay/light will turn ON/OFF based on your browser schedule!

---

## 🔎 How It Works

| Step | Description |
|:----:|:------------|
| 1 | User schedules ON/OFF time via the browser UI |
| 2 | WebSocket server receives it and sends to MQTT broker |
| 3 | `light-scheduler.py` subscribes and listens for schedules |
| 4 | Sends ON/OFF command to Arduino via Serial |
| 5 | Arduino toggles the light/relay accordingly |

---

## 💡 Notes

- `loop://` is used for simulation when real hardware is unavailable.
- Scheduling automatically resets daily at midnight (00:00).
- Make sure you import `serial.urlhandler.protocol_loop` for the simulation to work!

---

## 📬 Contact

**Created by**: Izere Shema Leandre ✍️  
📧 **Email**: [iamshemaleandre@gmail.com](mailto:iamshemaleandre@gmail.com)

---

