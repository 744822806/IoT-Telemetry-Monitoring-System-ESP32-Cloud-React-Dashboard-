IoT Telemetry & Monitoring System (ESP32 → Cloud Backend → React Dashboard)

A complete end-to-end IoT telemetry pipeline that collects sensor data on an ESP32, uploads it to a cloud backend, stores it in MongoDB Atlas, and visualizes real-time metrics through a modern React dashboard.

This project demonstrates a full-stack IoT architecture covering embedded firmware, cloud services, real-time data streaming, and UI visualization.

🚀 Features
Embedded Firmware (ESP32 + FreeRTOS + C)

Custom BMP280 I²C driver implemented at register level.

Dual-task FreeRTOS architecture for deterministic sampling and network uploading.

Real-time timestamping using esp_timer.

HTTP JSON telemetry uploader with reconnect logic.

Stable 2 Hz sampling with <100 ms end-to-end latency.

Cloud Backend (Node.js + Express + MongoDB Atlas)

REST API ingestion endpoint for ESP32 devices.

MongoDB Atlas cloud database for telemetry storage.

Real-time updates to UI clients using Socket.IO.

Modular routing and model structure.

Frontend Dashboard (React + Chart.js)

Displays current temperature and real-time chart of last 20 readings.

Clean, modern UI with responsive layout.

Polling + API integration for reliable updates.

🧩 System Architecture
BMP280 Sensor
      │ I²C
      ▼
 ESP32 Firmware (C · FreeRTOS)
  - BMP280 Driver
  - Sensor Task (producer)
  - Wi-Fi/Upload Task (consumer)
  - HTTP JSON Upload

      │ Wi-Fi
      ▼
 Cloud Backend (Node.js)
  - Express API
  - MongoDB Atlas Storage
  - Socket.IO Real-Time Push

      │ WebSocket / HTTP
      ▼
 Frontend Dashboard (React)
  - Current Temperature
  - Trend Visualization (Chart.js)

📁 Repository Structure
firmware/
   main.c
   bmp280.c
   bmp280.h
   wifi_http.c
   wifi_http.h
   CMakeLists.txt

backend/
   app.js
   models/
      Reading.js
   routes/
      readings.js

frontend/
   src/
      App.jsx

⚙️ Setup Instructions
1. Firmware (ESP32 + ESP-IDF)
cd firmware
idf.py set-target esp32
idf.py build flash monitor


Edit Wi-Fi credentials in wifi_http.c:

#define WIFI_SSID "YOUR_WIFI"
#define WIFI_PASS "YOUR_PASS"

2. Backend (Node.js + MongoDB)
cd backend
npm install
node app.js


Your backend will run on:

http://localhost:4000

3. Frontend (React)
cd frontend
npm install
npm start


Dashboard runs at:

http://localhost:3000

📊 Performance

2 Hz telemetry sampling

<100 ms device-to-UI latency

Zero data loss under multi-minute continuous operation

🧑‍💻 Tech Stack
Embedded

ESP32 · ESP-IDF · FreeRTOS · I²C · C · HTTP JSON

Backend

Node.js · Express · MongoDB Atlas · WebSockets (Socket.IO)

Frontend

React · Chart.js · Axios
