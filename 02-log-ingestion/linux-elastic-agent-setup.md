# Linux Elastic Agent Deployment & Log Ingestion

## 📌 Objective
To install Elastic Agent on the Ubuntu SSH server and enable centralized Linux log ingestion into Elasticsearch for SOC monitoring and DFIR investigations.

This deployment enabled:
- Linux telemetry collection
- SSH authentication monitoring
- Centralized log visibility in Kibana
- Querying Linux security events within Elasticsearch

---

# ☁️ Environment Overview

| Component | Details |
|---|---|
| Endpoint Name | `MyDFIR-Linux-Tee` |
| Operating System | Ubuntu 24.02 |
| Public IP Address | `155.138.143.139` |
| SIEM Platform | Elastic Stack (ELK) |

---

# 🖥️ Elastic Agent Deployment

## 📌 Objective
To onboard the Ubuntu SSH server into Elastic Fleet for centralized monitoring and log ingestion.

---

# ⚙️ Fleet Policy Configuration

Logged into Kibana and navigated to:
Management → Fleet → Agent Policies

---
# 🔹 Created Linux Agent Policy

Created a new Fleet policy:

Field               	Value
Policy Name       	MyDFIR-Linux-Policy

This policy was created specifically for Linux SSH monitoring and telemetry collection.

---

# 📡 Agent Enrollment

Navigated to:

Fleet → Agents → Add Agent

Selected:

MyDFIR-Linux-Policy

Copied the generated Elastic Agent installation command.

---
# ▶️ Elastic Agent Installation

Connected to the Ubuntu server and executed the installation command with the --insecure flag.

Example format:

sudo ./elastic-agent install --url=https://<FLEET_SERVER>:8220 --enrollment-token=<TOKEN> --insecure

## ✅ Enrollment Verification

Confirmed:

- Elastic Agent installation completed successfully
- Agent enrollment confirmed
- Linux endpoint appeared within Kibana Fleet

---

## 🔍 Log Ingestion Verification

Opened Kibana Discover and verified Linux authentication logs were successfully ingested into Elasticsearch.

---

# 🔹 Linux Authentication Visibility

Queried authentication-related events and observed:

- SSH login activity
- Failed password attempts
- Authentication logs from /var/log/auth.log

This confirmed successful Linux telemetry ingestion.

---

## 🚨 Authentication Failure Analysis

Performed searches against ingested Linux authentication events to identify failed SSH login attempts.

These logs provide visibility into:

Brute-force activity
Unauthorized access attempts
SSH authentication failures
Suspicious remote login behavior

## ✅ Verification

Confirmed:

- Elastic Agent successfully installed on Ubuntu server
- Linux endpoint enrolled into Fleet
- Authentication logs ingested into Elasticsearch
- Linux telemetry searchable within Kibana Discover
- Failed SSH attempts visible in queries

## 🔹 Linux Elastic Agent Enrollment
![Linux Agent Enrollment](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/linux-agent-enrollment.png)

---

## 🔹 Linux Fleet Agent
![Linux Fleet Agent](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/linux-fleet-agent.png)

---

## 🔹 Linux Discover Logs
![Linux Discover Logs](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/linux-discover.png)

---

## 🔹 Authentication Failure Search
![Linux Auth Failures](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/linux-auth-failures.png)

## 🔐 Security Considerations

The following considerations were implemented:

- Centralized Linux telemetry collection
- SSH authentication visibility
- Monitoring of failed login attempts
- Endpoint enrollment through Fleet-managed architecture

---
## 🎯 Key Takeaways
- Successfully deployed Elastic Agent on Ubuntu Linux
- Enrolled Linux endpoint into Fleet
- Enabled centralized Linux authentication monitoring
- Verified Elasticsearch ingestion for SSH-related telemetry
- Established Linux visibility for SOC monitoring and DFIR investigations

This deployment expanded the SOC environment into multi-platform telemetry monitoring and enabled centralized analysis of Linux authentication activity.
