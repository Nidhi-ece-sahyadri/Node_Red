## node red
---
# 🌡️ ESP32 Temperature Monitor with Node-RED (No MQTT)

This project allows an **ESP32** to send temperature data to a **Node-RED** server using **HTTP POST** (not MQTT), and displays the data in real-time on a gauge dashboard.

---

## 🚀 Features

- 📡 Sends temperature data over HTTP
- 📊 Real-time dashboard display using Node-RED
- 🧠 No MQTT needed
- 🔄 Updates every 5 seconds

---

## 🛠️ Requirements

- ESP32 board
- Arduino IDE
- Node.js installed
- Node-RED installed
- `node-red-dashboard` installed
- ESP32 and PC on the same Wi-Fi network

---

## 🧰 Installation Steps

### 1. Install Node.js and Node-RED

- Download and install [Node.js](https://nodejs.org/)
- Then install Node-RED globally:
  ```bash
  npm install -g --unsafe-perm node-red
---
## 2. Install Node-RED Dashboard
- Run this command in your terminal:
    ```bash
   npm install node-red-dashboard
  ---
 ## 3. Start Node-RED
- Start Node-RED by running:
    ```bash
   node-red
- Then open the Node-RED editor in your browser:
     ```bash
  http://localhost:1880
---
  ## 📥 Node-RED Flow Setup
📌 Flow Structure:

  <img width="1052" height="267" alt="Screenshot 2025-07-19 120543" src="https://github.com/user-attachments/assets/9bfb9a68-9fc0-4fd1-8015-123a07ae7eb2" />

  
