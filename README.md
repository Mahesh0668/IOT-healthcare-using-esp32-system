# IoT Healthcare Monitoring System using ESP32 & FreeRTOS

Dual-core ESP32 healthcare monitoring system featuring real-time vitals tracking, threshold safety alarms, remote bed elevation control, adaptive sampling, and fault-tolerant offline buffering via Adafruit IO.

---

## 🔗 Quick Project Links

* **Live Wokwi Simulation:** [Open Wokwi Project](PASTE_YOUR_WOKWI_SHARE_LINK_HERE)
* **Demo Video (MP4 / Drive):** [Watch Video Demonstration](PASTE_YOUR_GOOGLE_DRIVE_VIDEO_LINK_HERE)
* **Medical Staff Dashboard:** [Open Adafruit IO Dashboard](PASTE_YOUR_STAFF_DASHBOARD_LINK_HERE)
* **Facility Management Dashboard:** [Open Adafruit IO Dashboard](PASTE_YOUR_FACILITY_DASHBOARD_LINK_HERE)
* **Full Reports & Deliverables Folder:** [Open Google Drive Folder](PASTE_YOUR_GOOGLE_DRIVE_FOLDER_LINK_HERE)

---

## 📁 Repository Structure & Tasks

* **[Task 1: Sensor Interfacing & Local Display](./Task-1/)** — Potentiometer vitals/AQI, DHT22 temp, and SSD1306 OLED interface.
* **[Task 2: Dual-Core RTOS & Local Safety Alerts](./Task-2/)** — High-priority safety loops on Core 1 with 1200 Hz buzzer and LED indicators.
* **[Task 3: Cloud Telemetry & Reconnection Loop](./Task-3/)** — Non-blocking MQTT streaming and exponential backoff retry on Core 0.
* **[Task 4: Intelligent Remote Bed Elevation Control](./Task-4/)** — Smooth servo ramping (0–90°) with clinical presets and distress overrides.
* **[Task 5: Smart Dynamic Sampling Rate](./Task-5/)** — Adaptive rate switching (5s distress / 20s stable) via FreeRTOS queues.
* **[Task 6: Fault-Tolerant Offline Data Buffering](./Task-6/)** — Local FIFO queue retaining data during network outages, flushing automatically upon reconnection.

---

## 📡 MQTT Architecture (Strict 3-Feed Constraint)
* `status-1` (Uplink): Cyclically multiplexes Heart Rate (BPM), Air Quality (AQI), Ward Temp (°C), and Bed Angle.
* `alarm-status` (Uplink): Transmits `ALL_CLEAR` or specific diagnostic alarms (`HIGH AQI`, `HIGH TEMP`, `VITAL ALERT`, `AUTO: BREATHING`).
* `control-1` (Downlink): Receives sampling rate override (5–60s / 0=Auto) and remote bed angles (0–90° / -1=Auto).
