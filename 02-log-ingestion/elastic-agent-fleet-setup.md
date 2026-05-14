02-log-ingestion/elastic-agent-fleet-setup.md
# Elastic Agent & Fleet Server Deployment

## 📌 Objective
To deploy a centralized Fleet Server for Elastic Agent management and onboard a Windows endpoint for centralized log collection and monitoring within the SOC/DFIR environment.

This phase enabled:
- Centralized agent management
- Endpoint log collection
- Windows telemetry ingestion
- SIEM visibility through Kibana Discover

---

# ☁️ Environment Overview

| Component | Details |
|---|---|
| Fleet Server OS | Ubuntu 22.04 |
| Fleet Server Public IP | `149.248.57.8` |
| Endpoint OS | Windows Server 2022 |
| SIEM Platform | Elastic Stack (ELK) |

---

# 🖥️ Fleet Server Deployment

## 📌 Objective
To deploy an Elastic Fleet Server responsible for managing Elastic Agents across the environment.

---

## 🔹 Deployment Steps

1. Deployed Ubuntu 22.04 server in Vultr
2. Installed Elastic Agent package
3. Configured the server as a Fleet Server
4. Connected Fleet Server to Elasticsearch and Kibana
5. Verified successful Fleet Server enrollment

---

# 🔐 Fleet Server Role

The Fleet Server is responsible for:
- Managing Elastic Agents
- Distributing configurations and integrations
- Receiving endpoint telemetry
- Maintaining centralized control of monitored systems

---

# 🪟 Windows Endpoint Enrollment

## 📌 Objective
To onboard the Windows Server 2022 endpoint into Fleet for centralized log ingestion and monitoring.

---

## 🔹 Enrollment Process

1. Installed Elastic Agent on the Windows server
2. Used Fleet enrollment command generated from Kibana
3. Connected the Windows endpoint to the Fleet Server
4. Verified successful enrollment in Kibana Fleet Management

---

# 📡 Log Ingestion Verification

After successful enrollment:

- Windows telemetry began forwarding to Elasticsearch
- Endpoint logs became visible in Kibana Discover
- Agent status displayed as healthy in Fleet

---

# 🔎 Kibana Discover Validation

Confirmed successful log ingestion by:
- Opening Kibana Discover
- Filtering endpoint logs
- Verifying incoming Windows telemetry events

This validated:
- Fleet connectivity
- Elastic Agent communication
- Elasticsearch indexing functionality

---

# ✅ Verification

Confirmed:
- Fleet Server operational
- Windows Elastic Agent enrolled successfully
- Agent status visible in Kibana Fleet
- Endpoint logs successfully ingested into Elasticsearch
- Logs searchable within Kibana Discover

---

# 📸 Screenshots

## 🔹 Fleet Agents Overview
![Fleet Agents](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/fleet-agents.png)

---

## 🔹 Kibana Discover Logs
![Discover Logs](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/discover-logs.png)

---

# 🔐 Security Considerations

The following security measures were considered during deployment:

- Centralized management of endpoint agents
- Controlled communication between Fleet Server and endpoints
- Visibility into Windows endpoint activity
- Secure telemetry forwarding into Elasticsearch

---

# 🎯 Key Takeaways

- Successfully deployed a centralized Fleet Server infrastructure
- Enrolled Windows endpoint into Elastic Fleet
- Enabled centralized telemetry collection
- Verified real-time log ingestion into Elasticsearch
- Established the foundation for threat detection, endpoint monitoring, and DFIR investigations

This deployment marked the transition from infrastructure setup into active SOC monitoring and endpoint visibility operations.
