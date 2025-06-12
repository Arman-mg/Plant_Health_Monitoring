# 🌿 Smart IoT Platform for Plant Health & Irrigation Management

This project implements an **IoT-based intelligent system** for **monitoring plant health** and managing **automated irrigation**. It integrates sensor data, machine learning models, and cloud services to optimize plant care using modern technologies such as MQTT, Flask APIs, Telegram Bot, and ThingSpeak.

---

## 🚀 Project Objective

To build a scalable, secure, and intelligent IoT system that:

* Monitors plant health through image-based disease detection
* Manages smart irrigation based on soil moisture and temperature
* Notifies users via a Telegram Bot and allows remote control
* Stores and visualizes sensor data using ThingSpeak
* Provides centralized communication through a REST-based catalog

---

## 📂 Directory Structure Overview

```
project/
│
├── Catalog/                     # Main service registry with REST APIs
│   ├── Dockerfile
│   ├── HomeCatalog.py
│   ├── Scale.py
│   ├── catalog.json
│   └── requirements.txt
│
├── Connectors/                  # Device drivers and MQTT setup per user/plant, Sensor registration & data collection
│   ├── user_1/
│   │   └── plant_1/
│   │       ├── Abstract_Device_Connector.py
│   │       ├── Device_Connector_humidity.py
│   │       ├── Device_Connector_moisture.py
│   │       ├── Device_Connector_temperature.py
│   │       ├── MyMQTT.py
│   │       └── configs.json
│   ├── user_2/
│   │   └── plant_1/
│   │       ├── Abstract_Device_Connector.py
│   │       ├── Device_Connector_humidity.py
│   │       ├── Device_Connector_moisture.py
│   │       ├── Device_Connector_temperature.py
│   │       ├── MyMQTT.py
│   │       └── configs.json
│
├── Controllers/                 # Health & irrigation decision systems
│   └── user_X/plant_X/...
│
├── Models/                      # ML models used for irrigation & disease detection
│   ├── Linear_regression_model.pkl
│   ├── irrigation_decision.h5
│   └── model.jpg
│
├── Telegram/                    # Telegram bot interface for remote monitoring
│   ├── MyMQTT.py
│   ├── Telegram_Bot.py
│
├── ThinkSpeak/                  # MQTT publisher and ThingSpeak adapter per user/plant, ThinkSpeak MQTT adapter & data streamer
│   ├── user_1/
│   │   └── plant_1/
│   │       ├── MyMQTT.py
│   │       ├── ThinkSpeakAdapter.py
│   │       └── configs.json
│   ├── user_2/
│   │   └── plant_1/
│   │       ├── MyMQTT.py
│   │       ├── ThinkSpeakAdapter.py
│   │       └── configs.json
│
├── irrigation_decision/
│   ├── data.csv
│   └── model.py
│
├── images/                      # Example images for disease detection
│   └── tomato.jpeg, TomatoHealthy2.JPG
│
├── IOT_presentation.pdf         # Project overview slides
├── README.md
├── iot.yml                      # Configuration/deployment descriptor
```

---

## 🧠 System Components

### 📘 **Catalog Service**

Acts as a central directory of all devices, services, and communication topics via REST API. Manages:

* Users and plant registrations
* Service routes (MQTT, Flask APIs)
* Real-time update of operational devices

### 📡 **Device Connector**

Handles data collection from sensors for each user/plant, and publishes it to MQTT and ThinkSpeak channels.

### 💧 **Irrigation Control**

Processes temperature and soil moisture data using:

* A **neural network** for irrigation decisions
* A **linear regression** model to predict irrigation duration

> *Depends on the health control API (Flask server on EC2) to be running.*

### 🌿 **Health Control**

* Captures plant leaf images and sends them to an EC2-hosted Flask API
* The API uses a **leaf disease classification model (InceptionV3)** to determine the plant’s health status

### 💬 **Telegram Bot**

A simple bot that allows users to:

* Log in and track plant status
* Check health and irrigation updates
* Trigger irrigation remotely
* Log out securely

### ☁️ **ThinkSpeak Adapter**

Streams real-time sensor data to ThingSpeak for storage and visualization. Improves system scalability and third-party integration.

---

## 🔒 Security Features

* MQTT communication encrypted with **Fernet (AES + HMAC)**
* User passwords hashed using **SHA-256** before being stored
* Ensures confidentiality and integrity across the system

---

## 💡 Usage Instructions

* **Connectors** folder: Add or configure sensor devices per user/plant.
* **Controllers** folder: Hosts logic for irrigation and health modules.
* **irrigation\_decision/model.py**: Contains the full ML pipeline for irrigation.
* **Telegram Bot**: To run the bot, execute `Telegram_Bot.py` and interact via `/login`, `/plant_id`, `/irrigation_status`, etc.

⚠️ **Note:** Health status detection requires the external EC2-based API to be deployed and accessible. 

## 📈 Future Improvements

* Add Docker Compose for easier deployment of all components
* Implement a web dashboard to complement Telegram
* Add multi-plant image segmentation support
* Automate health model deployment via CI/CD