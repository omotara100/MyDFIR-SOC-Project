# Sysmon Deployment & Telemetry Verification

## 📌 Objective
To install Sysmon on the Windows Server 2022 endpoint and enable advanced Windows telemetry collection for threat detection, DFIR investigations, and endpoint monitoring.

Sysmon provides enhanced visibility into:
- Process creation
- Network connections
- PowerShell activity
- File creation events
- Persistence mechanisms
- Suspicious system activity

---

# 🪟 Environment Details

| Component | Details |
|---|---|
| Endpoint OS | Windows Server 2022 |
| Public IP | `149.248.56.62` |
| Sysmon Version | v15.2 |

---

# 🌐 Remote Access

Connected remotely to the Windows Server using RDP.

---

## 🔹 RDP Connection

Established a remote session to:
149.248.56.62

## 📥 Sysmon Installation
🔹 Download Sysmon

Downloaded Sysmon v15.2 from the official Microsoft Sysinternals website.

## 🔹 Extract Files

Extracted the Sysmon package on the Windows server.

The extracted files included:

- Sysmon64.exe
- EULA documentation
- Supporting binaries

## ⚙️ Sysmon Configuration
🔹 Download Sysmon Configuration

Downloaded the Sysmon configuration file from the Olaf Hartong Sysmon configuration repository on GitHub.

Selected:
sysmonconfig.xml

Saved the raw XML configuration file locally on the Windows server.

## ▶️ Install Sysmon with Configuration

Opened PowerShell as Administrator and installed Sysmon using the configuration file:

.\sysmon64.exe -i sysmonconfig.xml

## 🔍 Telemetry Verification

Verified successful Sysmon installation using Windows Event Viewer.

🔹 Event Viewer Path

Navigated to:

Applications and Services Logs
→ Microsoft
→ Windows
→ Sysmon
→ Operational

Confirmed:

- Sysmon service operational
- Telemetry events successfully generated
- Endpoint logging functioning correctly

## 🧠 Why Sysmon Matters

Sysmon significantly improves endpoint visibility compared to default Windows logging.

It enables:

- Advanced threat hunting
- Malware analysis
- PowerShell monitoring
- Detection engineering
- MITRE ATT&CK mapping
- Incident investigation workflows

This telemetry becomes critical for SOC operations and DFIR analysis.

## ✅ Verification

Confirmed:

Sysmon service installed successfully
Sysmon operational logs visible in Event Viewer
Telemetry generation functioning correctly
Endpoint ready for Elasticsearch ingestion

## 🔹 Sysmon Service
![Sysmon Service](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/sysmon-service.png)

---

## 🔹 Sysmon Event Viewer Logs
![Sysmon Event Viewer](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/sysmon-event-viewer.png)

## 🔐 Security Considerations

The following considerations were implemented:

- Enhanced endpoint telemetry collection
- Visibility into suspicious system behavior
- Monitoring of process execution activity
- Increased detection capability for malicious actions

## 🎯 Key Takeaways
- Successfully deployed Sysmon on a Windows Server 2022 endpoint
- Configured advanced Windows telemetry collection
- Verified operational event logging
- Prepared endpoint telemetry for centralized ingestion into Elasticsearch

This deployment significantly improved endpoint visibility and established the foundation for advanced threat detection and DFIR investigations within the SOC environment.
