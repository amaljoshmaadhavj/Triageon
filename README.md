# TRIAGEON

[![Python Version](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![Node.js Version](https://img.shields.io/badge/Node.js-16+-green.svg)](https://nodejs.org/)
[![Status](https://img.shields.io/badge/Status-Active-brightgreen.svg)](https://github.com)
[![Last Updated](https://img.shields.io/badge/Updated-2026-blue.svg)]()

> **ML-Driven Urgency-Aware Digital Health Triage System**

## Overview

TRIAGEON is an end-to-end, machine-learning–powered digital triage platform designed to identify medical risk early, classify patient urgency accurately, and guide patients toward appropriate care. It focuses on **risk detection and prioritization**, not final diagnosis, ensuring safety, scalability, and real-world clinical usability.

The system is especially targeted toward **rural and semi-urban healthcare environments**, where delayed detection of serious conditions often leads to avoidable complications.

---

## Problem Statement

Healthcare systems frequently suffer from:

* Overcrowding by non-urgent cases
* Missed or delayed identification of high-risk patients
* Poor understanding of lab reports by patients
* Lack of structured urgency assessment

Critical conditions such as anemia, diabetes, hypertension, heart disease, and severe infections often go unnoticed until they become life-threatening.

TRIAGEON addresses this gap using ML-based risk prediction, explainable urgency scoring, and proactive care navigation.

---

## Core Features

* **Multi-Condition Risk Assessment**: Prediction models for diabetes, hypertension, heart disease, fever/infection, and anemia
* **Intelligent Triage System**: Automated urgency classification (Emergency/Red, Urgent/Orange, Monitor/Yellow, Self-Care/Green)
* **Explainable AI**: Clear, human-readable explanations of risk factors and recommendations
* **Comprehensive Patient Interface**: Symptom input, vital signs tracking, lab report analysis
* **Real-time Predictions**: Instantaneous risk scoring and department routing
* **Care Navigation**: Clinic recommendations and specialist mapping based on urgency level

---

## System Architecture

### Core Layers

#### 1. Frontend Layer (React + Vite)
- Patient onboarding and intake forms
- Symptom and vital signs input
- Lab report upload and display
- Real-time urgency visualization (urgency badges)
- Explainable risk reasoning display
- Clinic/specialist nearby finder
- Triage result presentation with care recommendations


#### 2. Backend API Layer (Node.js + Express)
- RESTful API endpoints for all ML services
- Request routing and orchestration
- CORS and security middleware
- Error handling and response formatting
- Database models for patients, predictions, and triage results


#### 3. ML Services Layer (Python + Flask)

**Disease-Specific Models:**
- **Diabetes Risk** (`ml-services/diabetes-risk/`) - Glucose and metabolic risk assessment
- **Blood Pressure/Hypertension** (`ml-services/bp-risk/`) - BP severity classification
- **Heart Disease** (`ml-services/heart-risk/`) - Cardiovascular risk scoring
- **Fever/Infection** (`ml-services/fever-risk/`) - Infection severity and fever analysis
- **Anemia Detection** (`ml-services/anemia-ai/`) - Hemoglobin estimation from eye images

**Fusion Engine** (`ml-services/fusion-engine/`) - Combines predictions from all models into unified triage decision

#### 4. Triage Engine

Urgency levels and response times:
- **RED (Emergency)**: Immediate medical attention - Critical conditions
- **ORANGE (Urgent)**: <10 minutes - Multiple serious risk factors
- **YELLOW (Monitor)**: 30-60 minutes - Moderate risk, needs observation
- **GREEN (Self-Care)**: Routine/home management - Low risk, preventive care

---

## Project Structure

```
Triageon/
├── backend/                    # Node.js Express API server
│   ├── src/
│   │   ├── app.js            # Express app configuration
│   │   ├── server.js         # Server entry point
│   │   ├── config/           # Configuration files (CORS, DB, env)
│   │   ├── controllers/      # Request handlers
│   │   ├── middleware/       # Custom middleware (auth, error, upload)
│   │   ├── models/           # Database schemas (MongoDB)
│   │   ├── routes/           # API route definitions
│   │   ├── services/         # Business logic and ML proxy
│   │   └── utils/            # Utility functions
│   └── package.json
│
├── frontend/                   # React + Vite frontend
│   ├── src/
│   │   ├── App.jsx           # Main app component
│   │   ├── main.jsx          # Entry point
│   │   ├── components/       # Reusable UI components
│   │   ├── pages/            # Page components
│   │   ├── services/         # API client services
│   │   ├── styles/           # CSS stylesheets
│   │   ├── utils/            # Utility functions and constants
│   │   └── assets/           # Images and media
│   ├── vite.config.js        # Vite configuration
│   └── package.json
│
├── ml-services/              # Python ML microservices
│   ├── diabetes-risk/        # Diabetes prediction model
│   ├── bp-risk/              # Hypertension/BP risk model
│   ├── heart-risk/           # Heart disease risk model
│   ├── fever-risk/           # Fever/infection severity model
│   ├── anemia-ai/            # Anemia detection model
│   └── fusion-engine/        # Unified triage decision engine
│
├── docs/                     # Documentation
│   ├── API-Spec.md
│   ├── Architecture.md
│   ├── Deployment.md
│   └── ML-Integration.md
│
├── docker-compose.yml        # Docker orchestration
├── README.md                 # This file
└── LICENSE                   # License information
```

---

## Technology Stack

### Frontend
- **React 18+** with Hooks for state management
- **Vite** for fast build and development
- **React Router DOM** for navigation
- **Framer Motion** for animations
- **CSS3** with modern styling

### Backend
- **Node.js** with ES modules
- **Express.js** for REST API
- **MongoDB** with Mongoose ODM
- **Axios** for HTTP requests to ML services
- **CORS** for cross-origin requests
- **dotenv** for environment configuration

### Machine Learning
- **Python 3.8+**
- **Flask** for REST API endpoints
- **scikit-learn** for ML models
- **NumPy/Pandas** for data processing
- **OpenCV/PIL** for image processing (for anemia detection)
- **Tensorflow/PyTorch** (optional, for deep learning models)

### DevOps
- **Docker & Docker Compose** for containerization
- **Nodemon** for backend hot reload
- **Vite dev server** for frontend hot reload

---

## Getting Started

### Prerequisites
- Node.js 16+ and npm/yarn
- Python 3.8+
- Docker and Docker Compose (optional)
- MongoDB instance or MongoDB Atlas connection

### Installation Steps

#### 1. Clone the Repository
```bash
git clone <repository-url>
cd Triageon
```

#### 2. Backend Setup
```bash
cd backend
npm install
```

Create `.env` file:
```
PORT=3001
MONGODB_URI=mongodb://localhost:27017/triageon
FRONTEND_URL=http://localhost:5179
NODE_ENV=development
```

Start backend:
```bash
npm run dev       # Development with nodemon
# or
npm start         # Production
```

#### 3. Frontend Setup
```bash
cd frontend
npm install
```

Start frontend:
```bash
npm run dev       # Starts on http://localhost:5179
```

#### 4. ML Services Setup
Each ML service needs to be started independently:

```bash
# Diabetes Risk Service
cd ml-services/diabetes-risk
pip install -r requirements.txt
python service.py

# Blood Pressure Risk Service
cd ml-services/bp-risk
pip install -r requirements.txt
python app.py

# Heart Risk Service
cd ml-services/heart-risk
pip install -r requirements.txt
python heart_service.py

# Fever Risk Service
cd ml-services/fever-risk
pip install -r requirements.txt
python app.py

# Anemia AI Service
cd ml-services/anemia-ai
pip install -r requirements.txt
python app.py

# Fusion Engine (Triage Decision Service)
cd ml-services/fusion-engine
pip install -r requirements.txt
python triage_api.py
```

Expected ML Service Ports:
- Diabetes: `8002`
- Blood Pressure: `8003`
- Heart: `8004`
- Fever: `8005`
- Anemia: `8001`
- Fusion/Triage: `8000`

### Using Docker Compose (Optional)
```bash
docker-compose up -d
```

## Safety & Scope

⚠️ **IMPORTANT:** TRIAGEON is a **risk assessment and triage system**, NOT a diagnostic tool.

- ✅ It identifies risks and prioritizes patient urgency
- ❌ It does NOT provide medical diagnoses
- ❌ It does NOT replace professional medical judgment
- ✅ Clinical decisions remain with licensed professionals

Recommendations should always be reviewed by healthcare professionals before patient care decisions.

---

## Author & Contact

**Amaljosh Maadhav J**

- Email: [amal018josephmathi@gmail.com]
- LinkedIn: [https://www.linkedin.com/in/amaljoshmaadhavj/]
- GitHub: [https://github.com/amaljoshmaadhavj]