# ELK Stack Deployment (Elasticsearch Setup)

## 📌 Objective
To deploy and configure an Elasticsearch instance in a cloud environment for centralized log storage and analysis.

---

## ☁️ Environment Setup

### 🔹 Cloud Provider
- Vultr

### 🔹 Region
- Toronto, CA

### 🔹 Network Configuration
- VPC Network: `172.31.0.0/24`
- Instance added to private network for internal communication

---

## 🖥️ Server Deployment

### 🔹 Instance Details
- Name: MyDFIR-ELK
- OS: Ubuntu 22.04
- Public IP: `216.128.178.215`

---

## 🔐 Accessing the Server

Connected to the Elasticsearch server remotely using SSH from PowerShell:
ssh root@216.128.178.215

---

## 🔄 System Preparation

Updated and upgraded the Ubuntu server packages:
apt update && apt upgrade -y

## 📦 Elasticsearch Installation
1. Download Elasticsearch Package

Downloaded the Elasticsearch .deb package from the official Elastic website using wget.
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.x.x-amd64.deb

2. Install Elasticsearch

Installed the package using dpkg:
dpkg -i elasticsearch-8.x.x-amd64.deb
 
## ⚙️ Elasticsearch Configuration

Modified the Elasticsearch configuration file:
nano /etc/elasticsearch/elasticsearch.yml

Updated the following settings:
network.host: 216.128.178.X
http.port: 9200

## 🔹 Purpose of Changes
- Allowed Elasticsearch to listen on the server network interface
- Enabled HTTP communication on port 9200
- Prepared the server for remote management and log ingestion

## 🔥 Firewall Configuration

Configured a Firewall Group in Vultr to secure Elasticsearch access.

## 🔹 Firewall Rules
- Allowed inbound traffic only from my personal IP address
- Restricted unauthorized access to Elasticsearch

## 🔹 Security Benefit

This reduced the exposed attack surface while still allowing remote administration access.

## ▶️ Starting Elasticsearch Service

Reloaded system services and started Elasticsearch:

systemctl daemon-reload
systemctl enable elasticsearch
systemctl start elasticsearch

## ✅ Verification

Verified the Elasticsearch service status:
systemctl status elasticsearch

Confirmed:
Elasticsearch service was active
Service successfully started without errors

### 🔹 Elasticsearch Instance Deployment
![ELK Instance](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/Elasticsearch-Instance-Deployment.png)

### 🔹 Vultr VPC Configuration
![VPC Setup](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/Vultr-VPC-Configuration.png)

## 🎯 Key Takeaways
- Successfully deployed Elasticsearch in a cloud environment
- Configured private networking using Vultr VPC
- Implemented firewall restrictions for secure access
- Verified operational readiness of the SIEM backend infrastructure

This deployment established the foundation for centralized log collection, threat detection, and future SOC operations within the lab environment.
