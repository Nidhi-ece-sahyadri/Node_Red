# Node_Red
# 🌡️ ESP32 Temperature Monitor with Node-RED 

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
  
### 📦 Install Node-RED Dashboard

To enable the visual dashboard interface in Node-RED, you need to install the `node-red-dashboard` module.

Run the following command in your terminal:

```bash
npm install node-red-dashboard
---
