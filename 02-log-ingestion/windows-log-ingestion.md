# Windows Log Ingestion into Elasticsearch

## 📌 Objective
To ingest Sysmon and Windows Defender telemetry into Elasticsearch for centralized monitoring, threat detection, and DFIR investigations within the SOC environment.

This phase enabled:
- Advanced Windows telemetry collection
- Endpoint visibility within Kibana
- Security event monitoring
- Threat hunting and detection engineering capabilities

---

# ☁️ Environment Overview

| Component | Details |
|---|---|
| SIEM Platform | Elastic Stack (ELK) |
| Endpoint OS | Windows Server 2022 |
| Telemetry Sources | Sysmon & Windows Defender |
| Agent Management | Elastic Fleet |

---

# 🧩 Sysmon Log Ingestion

## 📌 Objective
To ingest Sysmon operational logs into Elasticsearch using Elastic integrations.

---

# ⚙️ Add Sysmon Integration

Logged into Kibana on the Elasticsearch instance and navigated to:

Management → Fleet → Integrations

# 🔹 Integration Selection

Selected:

Custom Windows Event Logs

This package allows ingestion from any Windows Event Log channel.

# 🔹 Sysmon Integration Configuration

Configured the integration with:

Field                    	Value
Integration Name	      MyDFIR-WIN-Sysmon
Description	            Sysmon telemetry ingestion
Channel Name          	Microsoft-Windows-Sysmon/Operational

# 🔹 Agent Policy Assignment

Added the integration to the existing Windows agent policy:

MyDFIR-Windows-Policy

Saved and deployed the configuration successfully.

## 🛡️ Windows Defender Log Ingestion
# 📌 Objective

To ingest Windows Defender operational logs into Elasticsearch for malware detection visibility.

# ⚙️ Add Windows Defender Integration

Repeated the same integration process using:

Custom Windows Event Logs

## 🔹 Defender Integration Configuration

Configured the integration with:
    
Field	                   Value
Integration Name	       MyDFIR-WIN-Defender
Description            	 Windows Defender telemetry ingestion
Channel Name	           Microsoft-Windows-Windows Defender/Operational

## 🎯 Windows Defender Event IDs

Configured the integration to ingest only the following Event IDs:

Event ID	       Description
1116	           Malware detected
1117	           Malware remediation action taken
5001	           Real-time protection disabled

These events provide visibility into:

- Malware detection activity
- Defender remediation operations
- Potential tampering or security control disabling

# 🔹 Advanced Integration Configuration

Within the integration Advanced Options section, added:

1116,1117,5001

This filtered ingestion to only relevant Defender security events.

## ❌ Issue Encountered

After configuration, logs were not appearing in Elasticsearch.

# 🛠️ Troubleshooting & Resolution

Investigation determined the issue was caused by firewall restrictions blocking Elasticsearch communication.

# 🔹 Firewall Fix

Modified firewall rules to allow:

Protocol	    Port
TCP          	9200

This restored communication between the Windows endpoint and Elasticsearch.

After updating the firewall:

- Sysmon logs successfully ingested
- Defender logs successfully ingested
- Events became searchable in Kibana Discover

## 🔍 Verification in Kibana Discover

Verified successful ingestion using Kibana Discover.

---

# 🔹 Sysmon Verification

Confirmed Sysmon telemetry using:

event.provider : "Microsoft-Windows-Sysmon"

Observed:

- Process creation events
- Network connection telemetry
- Endpoint activity logs

## 🔹 Windows Defender Verification

Confirmed Defender telemetry ingestion using:

event.provider : "Microsoft-Windows-Windows Defender"

Observed:

- Malware detection alerts
- Defender operational events
- Security protection status events

## ✅ Verification

Confirmed:

Sysmon integration operational
Windows Defender integration operational
Endpoint telemetry successfully ingested into Elasticsearch
Logs searchable within Kibana Discover
Fleet integrations deployed successfully

## 🔹 Sysmon Integration
![Sysmon Integration](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/sysmon-integration.png)

---

## 🔹 Windows Defender Integration
![Defender Integration](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/defender-integration.png)

---

## 🔹 Sysmon Discover Logs
![Sysmon Discover](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/sysmon-discover.png)

---

## 🔹 Windows Defender Discover Logs
![Defender Discover](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/defender-discover.png)

---

##  🔐 Security Considerations

The following considerations were implemented during telemetry ingestion:

- Filtered Defender logs to security-relevant Event IDs only
- Enhanced endpoint visibility using Sysmon
- Enabled centralized monitoring of malware-related activity
- Ensured secure communication between endpoints and Elasticsearch

## 🎯 Key Takeaways
Successfully ingested Sysmon telemetry into Elasticsearch
Successfully ingested Windows Defender operational logs
Configured selective event filtering for security-relevant Defender events
Troubleshot and resolved firewall-related ingestion issues
Enabled advanced endpoint visibility and DFIR telemetry collection

This phase completed the core Windows telemetry ingestion pipeline required for detection engineering, threat hunting, and SOC investigations.
