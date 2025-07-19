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
### 2. Install Node-RED Dashboard
- Run this command in your terminal:
- npm install node-red-dashboard

---

## 3. Start Node-RED
- Start Node-RED by running:
  node-red
- Then open the Node-RED editor in your browser:
  http://localhost:1880

  ---
  ## 📥 Node-RED Flow Setup
  -[POST /temperature]
         ↓
       [JSON]
       ↙   ↓   ↘
[Debug] [HTTP Response] [Gauge]

---
## 🧩 Node Configuration:
-HTTP In Node
Method: POST
URL: /temperature
-JSON Node
Name: Parse JSON
-Gauge Node
Value format: {{msg.payload.temperature}}
Label: {{value}} °C
Units: °C
Range: 0 - 100
-Debug Node
Output: msg.payload.temperature
-HTTP Response Node
Use to terminate the HTTP POST request

---

## 🌐 Dashboard Access
After deploying your flow, visit the dashboard:
http://<your-PC-IP>:1880/ui
-----

## JSON Formate 
[
  {
    "id": "1a1d21223aa31f3f",
    "type": "tab",
    "label": "Temperature Flow",
    "disabled": false,
    "info": ""
  },
  {
    "id": "bdc0d78dcf3d45f1",
    "type": "http in",
    "z": "1a1d21223aa31f3f",
    "name": "",
    "url": "/temperature",
    "method": "post",
    "upload": false,
    "swaggerDoc": "",
    "x": 140,
    "y": 120,
    "wires": [["6b6d297b3ecaa7de"]]
  },
  {
    "id": "6b6d297b3ecaa7de",
    "type": "json",
    "z": "1a1d21223aa31f3f",
    "name": "",
    "property": "payload",
    "action": "",
    "pretty": false,
    "x": 320,
    "y": 120,
    "wires": [["3b730b38268f41aa", "067b799dc0484970"]]
  },
  {
    "id": "3b730b38268f41aa",
    "type": "debug",
    "z": "1a1d21223aa31f3f",
    "name": "Temperature Debug",
    "active": true,
    "tosidebar": true,
    "console": false,
    "tostatus": false,
    "complete": "payload",
    "targetType": "msg",
    "statusVal": "",
    "statusType": "auto",
    "x": 540,
    "y": 100,
    "wires": []
  },
  {
    "id": "067b799dc0484970",
    "type": "ui_gauge",
    "z": "1a1d21223aa31f3f",
    "name": "Temperature Gauge",
    "group": "8f2f3c28793ecf23",
    "order": 0,
    "width": 0,
    "height": 0,
    "gtype": "gage",
    "title": "Temperature (°C)",
    "label": "°C",
    "format": "{{value}}",
    "min": "0",
    "max": "100",
    "colors": ["#00b500", "#e6e600", "#ca3838"],
    "seg1": "",
    "seg2": "",
    "className": "",
    "x": 550,
    "y": 160,
    "wires": []
  },
  {
    "id": "a8d3190f12d72e96",
    "type": "http response",
    "z": "1a1d21223aa31f3f",
    "name": "",
    "statusCode": "",
    "headers": {},
    "x": 540,
    "y": 220,
    "wires": []
  },
  {
    "id": "8f2f3c28793ecf23",
    "type": "ui_group",
    "name": "Room A",
    "tab": "5f8c109c8ec15b4d",
    "order": 1,
    "disp": true,
    "width": 6,
    "collapse": false,
    "className": ""
  },
  {
    "id": "5f8c109c8ec15b4d",
    "type": "ui_tab",
    "name": "Dashboard",
    "icon": "dashboard",
    "disabled": false,
    "hidden": false
  }
]

---
## Arduino IDE code
#include <WiFi.h>
#include <HTTPClient.h>

// 👉 Replace with your Wi-Fi credentials
const char* ssid = "SSID";
const char* password = "PWD";

// 👉 Replace with your PC's IP address where Node-RED is running
const char* serverUrl = "http://192.168.187.206:1880/temperature";
// <-- CHANGE THIS

void setup() {
  Serial.begin(115200);

  // Connect to Wi-Fi
  WiFi.begin(ssid, password);
  Serial.print("Connecting to Wi-Fi");

  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }

  Serial.println("\nConnected to Wi-Fi!");
  Serial.print("ESP32 IP Address: ");
  Serial.println(WiFi.localIP());
}

void loop() {
  if (WiFi.status() == WL_CONNECTED) {
    HTTPClient http;

    http.begin(serverUrl);
    http.addHeader("Content-Type", "application/json");

    // Simulated temperature value
    float temp = random(200, 350) / 10.0; // 20.0°C to 35.0°C

    // Create JSON string
    String jsonData = "{\"sensor\":\"ESP32\",\"location\":\"Room A\",\"temperature\":" + String(temp, 1) + "}";

    // Send POST request
    int httpResponseCode = http.POST(jsonData);

    // Print response
    Serial.print("HTTP Response code: ");
    Serial.println(httpResponseCode);
    Serial.println("Sent: " + jsonData);
    Serial.println("------");

    http.end();
  } else {
    Serial.println("Wi-Fi not connected.");
  }

  delay(5000); // Wait 5 seconds before sending again
}


