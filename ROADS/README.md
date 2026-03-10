# Dynamic AI Traffic Flow Optimizer & Emergency Corridor System

An AI-powered intelligent traffic management system that combines computer vision, real-time traffic analytics, and adaptive signal control to optimize traffic flow and create priority green corridors for emergency vehicles.

---

# Overview

This system analyzes live traffic using computer vision models and calculates a **Comprehensive Priority Score (CPS)** for each intersection signal.
Based on this score, the system dynamically adjusts signal timings and enables **green corridor routing for emergency vehicles**.

The goal is to reduce congestion, improve traffic safety, and allow emergency vehicles like **ambulances and fire trucks** to move through intersections without delays.

---

# System Workflow

Traffic Cameras → Vehicle Detection → Traffic Feature Extraction → Priority Decision Engine → Green Time Calculation → Traffic Signal Control

1. Traffic cameras capture real-time road footage.
2. YOLO-based computer vision detects and tracks vehicles.
3. Traffic metrics (density, speed, violations, queue length) are extracted.
4. A Priority Decision Engine calculates a **Comprehensive Priority Score (CPS)**.
5. The system computes optimal green signal duration.
6. Traffic signals are adjusted dynamically.

---

# Core Components

## 1. Computer Vision Layer

Uses **YOLO object detection and ByteTrack tracking** to analyze traffic footage.

Capabilities:

* Vehicle detection and classification
* Vehicle counting
* Speed estimation
* Queue length estimation
* Hard braking detection
* Tailgating detection
* Emergency vehicle detection

---

## 2. Traffic Feature Extraction

The system extracts key metrics from each video stream:

* Total vehicle count
* Vehicle class distribution
* Average speed
* Queue length
* Hard braking events
* Tailgating violations
* Platoon movement behavior

---

## 3. Comprehensive Priority Score (CPS)

The CPS determines which signal should receive priority green time.

### Formula

CPS = Traffic Score − Safety Penalty + Green Wave Bonus

### Components

**Traffic Score**
Represents traffic density weighted by vehicle type importance.

Vehicle Weights:

* Ambulance → 12
* Bus → 3.5
* Truck → 2.5
* Car → 1
* Bike → 0.3

Contribution: **65%**

---

**Safety Penalty**

Reduces priority if unsafe driving behaviors are detected.

Factors:

* Hard braking events
* Tailgating events

Contribution: **12%**

---

**Green Wave Bonus**

Provides priority boost for approaching emergency vehicles.

Factors:

* Distance to intersection
* Average speed
* Estimated arrival time (ETA)

Contribution: **23%**

---

# Green Time Calculation

The system calculates the green signal duration based on queue length and lane count.

Steps:

1. Estimate number of vehicle rows.
2. Apply discharge headway timing.
3. Compute clearance time required.

Example discharge timings:

Row 1 → 3.8s
Row 2 → 3.1s
Row 3 → 2.7s
Row 4 → 2.2s
Additional rows → 2.1s each

Output:

* Queue rows
* Required green signal time

---

# Backend API

The backend is implemented using **FastAPI**.

Example Endpoints:

GET /
Returns API status.

POST /intersection1/traffic{signal_id}
Processes traffic data and returns CPS score and signal timing.

GET /intersection1
Returns aggregated intersection traffic data.

---

# Technology Stack

Programming Language: Python
Computer Vision: OpenCV
Object Detection: YOLO
Object Tracking: ByteTrack
Backend Framework: FastAPI
Data Models: Pydantic
Server: Uvicorn
Numerical Processing: NumPy

---

# Key Features

* Real-time traffic monitoring
* AI-based signal prioritization
* Emergency vehicle green corridor
* Safety violation detection
* Queue clearance estimation
* API-based scalable architecture

---

# Future Improvements

* Multi-intersection coordination
* Reinforcement learning signal optimization
* Integration with smart city infrastructure
* Real-time deployment with live CCTV feeds
* Traffic prediction using historical data

---

# Project Goal

This project demonstrates a **feasible and scalable AI-driven traffic management system** designed to:

* Reduce congestion
* Improve road safety
* Enable faster emergency response
* Support smart city infrastructure

