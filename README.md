# Smart Garden Management System (SGMS)

![Python](https://img.shields.io/badge/Python-3.8+-blue?style=flat-square) ![License](https://img.shields.io/badge/License-MIT-green?style=flat-square) ![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=flat-square)

## 📋 Overview

The **Smart Garden Management System (SGMS)** is an intermediate-level IoT-based garden automation system designed to revolutionize residential garden care. This project is a comprehensive demonstration of modern software engineering principles, IoT integration, and full-stack application development.

**Academic Context:** This project was developed as part of **Term-4 coursework** for the **Principles of Software Engineering (CAP314)** course at **Lovely Professional University (LPU)**, BBA Information Technology program.

### Key Features

- 🌱 **Real-time Monitoring**: IoT sensors track soil moisture, temperature, and ambient light
- 💧 **Automated Irrigation**: Intelligent watering system based on sensor data and plant requirements
- 📱 **Mobile Application**: User-friendly React Native app for monitoring and control
- 🌿 **Plant Database**: Tailored care recommendations for 100+ plant species
- 🌤️ **Weather Integration**: Real-time weather forecasts to optimize watering schedules
- 📊 **Data Analytics**: Comprehensive insights into garden health and water usage

---

## 🎯 Project Objectives

1. Develop a system to monitor soil moisture and environmental conditions in real-time using IoT sensors
2. Automate irrigation based on sensor data, plant requirements, and weather forecasts
3. Provide a mobile application for garden monitoring, control, and plant care insights
4. Integrate a plant database with tailored care recommendations
5. Ensure scalability, security, and optimal usability for diverse user needs

---

## 🏗️ System Architecture

### Architecture Overview

SGMS employs a **client-server architecture** with three main layers:

```
┌─────────────────────────────────────────────────────────┐
│                    Client Layer                         │
│           (React Native Mobile Application)             │
└──────────────────────┬──────────────────────────────────┘
                       │
                       │ HTTPS
                       │
┌──────────────────────▼──────────────────────────────────┐
│                    Backend Server                       │
│          (Node.js/Express.js + REST API)               │
└──────────────────────┬──────────────────────────────────┘
         │             │              │
      MQTT│        MongoDB        External
         │             │           APIs
┌────────▼──┐    ┌──────▼──┐  ┌──────────┐
│  IoT      │    │Database │  │OpenWeatherMap
│ Devices   │    │         │  │+ Trefle.io
└───────────┘    └─────────┘  └──────────┘
```

### Technology Stack

| Component | Technology |
|-----------|---------------------|
| **Frontend** | React Native, Expo |
| **Backend** | Node.js, Express.js |
| **Database** | MongoDB |
| **IoT Protocol** | MQTT (Mosquitto) |
| **Microcontroller** | ESP32 |
| **Sensors** | Capacitive soil moisture, DHT22 (temp/humidity) |
| **External APIs** | OpenWeatherMap, Trefle Plant API |
| **Deployment** | AWS (EC2 + MongoDB Atlas) |
| **Version Control** | Git & GitHub |

---

## 📊 System Design

### Functional Requirements

1. **Real-time Monitoring**
   - IoT sensors measure soil moisture, temperature, and light every 5 minutes
   - Real-time data displayed in graphical and tabular formats

2. **Automated Irrigation**
   - Watering triggered when moisture falls below plant-specific thresholds
   - Automatic schedule adjustment based on weather forecasts

3. **Mobile Application**
   - Real-time sensor data visualization
   - Manual watering override controls
   - Push notifications for anomalies

4. **Plant Database Integration**
   - 100+ common plant species
   - Personalized care instructions
   - Watering frequency and sunlight recommendations

### Non-Functional Requirements

- **Scalability**: Support up to 10 gardens per user, 50 sensors per garden
- **Security**: HTTPS encryption, AES-256 data encryption, JWT authentication
- **Performance**: <2s sensor update delivery, <1s watering decision processing
- **Reliability**: 99.9% server uptime with failover mechanisms
- **Usability**: Key functions accessible within 3 clicks

---

## 🔧 Implementation

### Project Structure

```
smart-garden-management-system/
├── backend/
│   ├── routes/
│   ├── controllers/
│   ├── models/
│   ├── middleware/
│   └── app.js
├── mobile-app/
│   ├── screens/
│   ├── components/
│   ├── navigation/
│   └── app.json
├── iot-firmware/
│   ├── sensor-read/
│   └── mqtt-publish/
├── docs/
│   ├── architecture.md
│   ├── api-documentation.md
│   └── deployment-guide.md
└── README.md
```

### Development Methodology

The project follows **Agile methodology** with 2-week sprints:

- **Sprint 1**: IoT sensor setup, MQTT communication
- **Sprint 2**: Backend API development, user authentication
- **Sprint 3**: Database schema, plant/weather integration
- **Sprint 4**: Mobile app dashboard and controls
- **Sprint 5**: Notifications system, comprehensive testing
- **Sprint 6**: UAT and deployment preparation

---

## 🚀 Deployment

### Deployment Strategy

- **Backend & Database**: AWS EC2 instance with MongoDB Atlas
- **Mobile App**: TestFlight (iOS) and APK distribution (Android)
- **IoT Devices**: ESP32 modules configured with local Wi-Fi and MQTT broker
- **CI/CD Pipeline**: GitHub Actions for automated testing and deployment

### Getting Started

1. Clone the repository
   ```bash
   git clone https://github.com/ujaan-chatterjee/smart-garden-management-system.git
   cd smart-garden-management-system
   ```

2. Set up the backend
   ```bash
   cd backend
   npm install
   npm start
   ```

3. Set up the mobile app
   ```bash
   cd mobile-app
   npm install
   expo start
   ```

---

## 📈 Key Metrics

- **Sensors Supported**: Up to 50 per garden
- **Plant Database**: 100+ species
- **Gardens per User**: Up to 10
- **API Response Time**: <2 seconds
- **System Uptime**: 99.9%

---

## 🤝 Contributing

This is an academic project. Contributions and suggestions are welcome!

---

## 📚 References

- IEEE Software Engineering Standards
- MQTT Protocol Specification
- MongoDB Documentation
- React Native Official Documentation
- OpenWeatherMap API
- Trefle Plant Database API

---

## 📄 License

MIT License - See LICENSE file for details

---

## 👤 Author

**Ujaan Chatterjee**
- GitHub: [@ujaan-chatterjee](https://github.com/ujaan-chatterjee)
- Email: itsujaan.chatterjee@gmail.com
- University: Lovely Professional University (LPU), BBA-IT

---

## ⭐ Acknowledgments

This project was inspired by similar IoT implementations and demonstrates core software engineering principles including requirements analysis, system design, implementation, testing, and deployment.

**Course**: Principles of Software Engineering (CAP314) | **Academic Year**: Term-4 | **Institution**: LPU
