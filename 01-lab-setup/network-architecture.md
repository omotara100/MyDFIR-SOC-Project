# Network Architecture Design

## 📌 Objective
To design a logical architecture for a simulated SOC/DFIR environment before deployment. This ensures proper segmentation, visibility, and realistic data flow between systems.

---

## 🧠 Overview
The lab environment is designed to simulate real-world SOC operations, including log ingestion, threat detection, attacker simulation, and incident response.

The architecture includes:
- SOC analyst access layer
- Cloud-hosted SIEM (ELK Stack)
- Endpoint systems generating logs
- Attack infrastructure for simulation
- Ticketing system for incident management

---

## 🏗️ Architecture Diagram

![Network Diagram](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/network-diagram.png)
---

## 🔧 Components Breakdown

### 🔹 SOC Analyst Machine
- Connects to Kibana via web interface
- Used for monitoring, investigation, and dashboard analysis

---

### 🔹 Vultr Cloud Environment (VPC)
- Private network: `172.31.0.0/24`
- Hosts all internal lab systems
- Provides isolation from public internet

---

### 🔹 ELK Stack Server
- Elasticsearch: stores logs
- Logstash: processes logs
- Kibana: visualization and analysis
- Central point for all log ingestion

---

### 🔹 Fleet Server
- Manages Elastic Agents
- Controls log collection from endpoints
- Ensures centralized agent management

---

### 🔹 Windows Server (RDP Enabled)
- Internet-facing Windows Server 2022 instance
- Used to simulate brute-force attacks and suspicious authentication activity
- Generates Windows event logs for ingestion into the ELK Stack
- Intentionally separated from the private VPC network to simulate an externally exposed endpoint

---

### 🔹 Ubuntu Server (SSH Enabled)
- Generates Linux logs
- Used for additional telemetry and attack surface

---

### 🔹 Ticketing Server
- Receives alerts from ELK
- Tracks incidents and investigations
- Simulates SOC workflow

---

### 🔹 Attacker Machine (Kali Linux)
- Used to simulate real-world attacks
- Performs brute-force, scanning, and exploitation

---

### 🔹 C2 Server (Mythic)
- Simulates command-and-control activity
- Used for advanced threat hunting scenarios

---

## 🔄 Data Flow

1. Endpoints (Windows & Ubuntu) generate logs
2. Logs are forwarded via Elastic Agents
3. Fleet Server manages agents
4. Logs are sent to Elasticsearch
5. Kibana is used for visualization and detection
6. Alerts are generated and sent to ticketing system
7. SOC analyst investigates alerts

---

## 🎯 Key Takeaways
- Centralized logging enables full visibility
- Segmented architecture improves realism
- Inclusion of attacker and C2 infrastructure allows advanced detection scenarios
- Ticketing integration simulates real SOC workflows
