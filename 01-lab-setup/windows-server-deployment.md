# Windows Server 2022 Deployment

## 📌 Objective
To deploy a Windows Server 2022 instance within the SOC/DFIR lab environment with Remote Desktop Protocol (RDP) exposed to the internet for remote administration and attack simulation scenarios.

This system will later be used to:
- Generate Windows security logs
- Simulate brute-force attacks
- Deploy Sysmon and Winlogbeat
- Monitor endpoint telemetry
- Conduct threat detection and investigation exercises

---

# ☁️ Environment Details

## 🔹 Cloud Provider
- Vultr

## 🔹 Operating System
- Windows Server 2022

## 🔹 Purpose
- Windows endpoint for SOC monitoring
- RDP attack simulation target
- Endpoint telemetry generation

---

# 🖥️ Server Deployment

## 🔹 Deployment Steps

1. Created a new Windows Server 2022 instance in Vultr
2. Attached the server to the existing VPC network
3. Assigned a public IP address
4. Enabled Remote Desktop Protocol (RDP) access

---

# 🌐 Remote Desktop Access

Connected remotely to the Windows server using Microsoft Remote Desktop.

## 🔹 RDP Connection

Used the server public IP address to establish a remote session:

```text
mstsc
