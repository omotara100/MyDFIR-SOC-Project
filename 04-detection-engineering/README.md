# 04 – Detection Engineering

## 📌 Overview

This section documents the detection engineering phase of the **MyDFIR-SOC-Project**, where telemetry generated from simulated attacks was transformed into actionable security detections, alerts, dashboards, and visualizations.

The objective was to develop practical SOC detection capabilities by creating custom rules, dashboards, and investigations using Elastic Security and Kibana.

This phase bridges the gap between **attack simulation** and **incident response**, demonstrating how security events can be identified, monitored, and escalated for investigation.

---

# 🎯 Objectives

- Develop custom detection rules using Elastic Security
- Build threshold-based alerts for brute-force attacks
- Create dashboards to monitor authentication activity
- Visualize attack sources using Kibana Maps
- Detect Mythic C2 malware execution
- Monitor suspicious process creation
- Detect outbound network communications
- Identify Microsoft Defender tampering
- Validate detections against live attack simulations

---

# 🔐 Detection Coverage

The following detection use cases were implemented throughout the project.

| Detection | Description |
|------------|-------------|
| SSH Brute Force | Detect repeated failed SSH authentication attempts |
| RDP Brute Force | Detect repeated failed Windows RDP authentication attempts |
| Mythic Apollo Execution | Detect execution of the Apollo C2 agent |
| Suspicious Process Creation | Monitor PowerShell, CMD, and Rundll32 execution |
| Outbound Network Connections | Detect processes initiating external communications |
| Microsoft Defender Disabled | Detect Event ID 5001 indicating Defender protection disabled |

---

# 🛠 Detection Technologies

| Technology | Purpose |
|------------|---------|
| Elastic Security | Detection rules and alerting |
| Kibana Discover | Log analysis |
| Kibana Dashboards | Visualization |
| Kibana Maps | Geolocation analysis |
| KQL | Detection queries |
| Sysmon | Endpoint telemetry |
| Windows Event Logs | Authentication monitoring |
| Linux Authentication Logs | SSH monitoring |

---

# 📊 Dashboards Created

The following dashboards were developed to support continuous monitoring.

## Authentication Dashboards

- SSH Failed Authentication
- SSH Successful Authentication
- RDP Failed Authentication
- RDP Successful Authentication

---

## Endpoint Monitoring

- Process Created (PowerShell, CMD, Rundll32)
- Process Created Initiated Network
- Microsoft Defender Disabled

---

## Geographic Visualization

- SSH Failed Authentication Map
- RDP Failed Authentication Map

These dashboards provide visibility into authentication activity, attacker source locations, endpoint behavior, and security control changes.

---

# 🚨 Detection Rules

Custom detection rules were created within Elastic Security.

| Rule | Severity |
|--------|----------|
| MyDFIR-SSH-Brute-Force-Attempt-Tee | Medium |
| MyDFIR-RDP-Brute-Force-Attempt-Tee | Medium |
| MyDFIR-Mythic-C2-Apollo | Critical |

The rules leverage Elastic's Detection Engine to generate alerts based on endpoint telemetry and authentication events.

---

# 📂 Documentation

## SSH Detection Engineering

- SSH authentication monitoring
- Threshold alert creation
- Dashboard development
- Geolocation visualization

📄 **File**

```text
ssh-bruteforce-alert.md
```

---

## Windows RDP Detection Engineering

- Windows authentication monitoring
- Event ID 4625 analysis
- Event ID 4624 correlation
- Detection rule creation
- Dashboard development

📄 **File**

```text
windows-rdp-bruteforce-alerts.md
```

---

## Mythic C2 Detection Engineering

- Apollo process detection
- SHA256 hash detection
- Original filename detection
- Network connection monitoring
- Microsoft Defender monitoring
- Malware-focused dashboards

📄 **File**

```text
mythic-c2-detection-engineering.md
```

---

# 📈 Detection Workflow

The detection engineering process followed the workflow below.

```text
Attack Simulation
        │
        ▼
Log Collection
        │
        ▼
Telemetry Ingestion
        │
        ▼
KQL Development
        │
        ▼
Detection Rule Creation
        │
        ▼
Alert Generation
        │
        ▼
Dashboard Visualization
        │
        ▼
Incident Investigation
```

---

# 🔍 MITRE ATT&CK Coverage

The implemented detections align with multiple MITRE ATT&CK tactics and techniques.

| Tactic | Techniques Covered |
|---------|-------------------|
| Initial Access | Brute Force (T1110) |
| Credential Access | Password Guessing (T1110.001) |
| Discovery | Account Discovery (T1033), System Information Discovery (T1082) |
| Execution | Command and Scripting Interpreter (T1059) |
| Defense Evasion | Impair Defenses (T1562.001) |
| Command & Control | Application Layer Protocol (T1071), Ingress Tool Transfer (T1105) |
| Exfiltration | Exfiltration Over C2 Channel (T1041) |

---

# 🧠 Skills Demonstrated

This phase demonstrates practical experience with:

- Detection Engineering
- Elastic Security
- Kibana Dashboards
- Kibana Maps
- KQL Query Development
- Sysmon Analysis
- Windows Event Log Analysis
- Linux Authentication Analysis
- Authentication Monitoring
- Process Monitoring
- Malware Detection
- Threat Detection
- Alert Tuning
- SIEM Operations
- MITRE ATT&CK Mapping

---

# 🎯 Key Outcomes

By completing this phase of the project, the following capabilities were successfully implemented:

- Centralized authentication monitoring
- Real-time brute-force detection
- Custom Elastic Security detection rules
- Endpoint process monitoring
- Network connection visibility
- Microsoft Defender tamper detection
- Malware execution detection
- Geolocation visualization of attack sources
- SOC-ready dashboards for continuous monitoring

These detections were validated against live attack simulations performed within the MyDFIR lab, providing practical experience with detection engineering and security operations workflows.

---

# 🔗 Next Phase

After detections were validated, alerts generated by Elastic Security were investigated as part of the Incident Response phase.

➡️ **Next Section**

```text
06-incident-response/
```

This phase documents the analyst investigation process, including alert triage, evidence collection, event correlation, and incident documentation.
