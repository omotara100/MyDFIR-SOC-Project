# 03 – Attack Simulation

## 📌 Overview

This section documents the attack simulation phase of the **MyDFIR-SOC-Project**, where realistic adversary techniques were executed against a controlled lab environment to generate security telemetry for detection engineering, threat hunting, and incident response.

Rather than relying on sample datasets, attacks were performed against cloud-hosted Windows and Linux systems to produce real endpoint and network events. These activities enabled the validation of custom detection rules, dashboards, and SOC investigation workflows built throughout the project.

The simulations were performed in an isolated lab environment for educational and defensive security purposes.

---

# 🎯 Objectives

The objectives of this phase were to:

- Simulate real-world attack techniques
- Generate endpoint and authentication telemetry
- Produce network activity for investigation
- Validate detection rules
- Test Elastic Security alerting
- Generate artifacts for threat hunting
- Support incident response investigations

---

# 🏗️ Attack Environment

| Component | Purpose |
|------------|----------|
| Kali Linux | Attacker workstation |
| Windows Server 2022 | Target Windows endpoint |
| Ubuntu 24.04 | Target Linux SSH server |
| Mythic C2 | Command & Control platform |
| Elastic Stack | Monitoring and detection |
| Sysmon | Endpoint telemetry |
| Microsoft Defender | Endpoint protection monitoring |

---

# 🗺️ Attack Lifecycle

The simulated attacks followed a structured attack lifecycle.

```text
Reconnaissance
        │
        ▼
Initial Access
        │
        ▼
Credential Attack
        │
        ▼
Successful Authentication
        │
        ▼
Discovery
        │
        ▼
Defense Evasion
        │
        ▼
Payload Execution
        │
        ▼
Command & Control
        │
        ▼
Data Exfiltration
```

---

# 🔐 Attack Scenarios

The following attack scenarios were completed.

## SSH Brute Force

A brute-force attack was performed against the Ubuntu SSH server to generate Linux authentication telemetry.

Objectives:

- Generate failed SSH authentication events
- Validate Elastic Security detections
- Populate authentication dashboards
- Support SOC investigations

---

## Windows RDP Brute Force

A brute-force attack was performed against the Windows Server using Remote Desktop Protocol (RDP).

Objectives:

- Generate Windows Event ID 4625
- Generate Windows Event ID 4624
- Validate RDP detection rules
- Produce authentication telemetry

---

## Host Discovery

Following successful authentication, host discovery activities were performed.

Activities included:

- User enumeration
- Network configuration review
- System information gathering

Example commands:

- whoami
- ipconfig
- net user

These activities generated endpoint telemetry for later investigation.

---

## Defense Evasion

Microsoft Defender Real-Time Protection was temporarily disabled within the controlled lab environment to simulate attacker attempts to impair endpoint protection.

Objectives:

- Generate Microsoft Defender Event ID 5001
- Validate Defender monitoring
- Produce detection opportunities

---

## Mythic Apollo Agent Deployment

The Apollo agent was deployed through the Mythic framework to simulate malware execution and establish command-and-control communications.

Objectives:

- Simulate malware execution
- Generate Sysmon Process Creation events
- Generate outbound network connections
- Validate custom malware detections

---

## Command & Control

The deployed Mythic agent successfully established communications with the Mythic C2 server.

Activities included:

- Agent registration
- Callback establishment
- Command execution
- Session management

---

## Data Exfiltration

A controlled file retrieval exercise was performed to simulate attacker data exfiltration.

Objectives:

- Demonstrate post-exploitation activity
- Generate endpoint telemetry
- Validate SOC investigations

---

# 📂 Documentation

The following documents describe each stage of the attack simulation.

| Document | Description |
|----------|-------------|
| `attacker-infrastructure.md` | Attacker architecture and attack lifecycle |
| `rdp-bruteforce-initial-access.md` | Initial access through RDP brute-force simulation |
| `mythic-c2-deployment.md` | Deployment of the Mythic C2 server |
| `mythic-agent-deployment.md` | Apollo agent deployment, C2 communication, and simulated data exfiltration |

---

# 🧠 MITRE ATT&CK Coverage

The simulations covered multiple MITRE ATT&CK tactics and techniques.

| Tactic | Techniques |
|---------|------------|
| Initial Access | T1110 – Brute Force |
| Credential Access | T1110.001 – Password Guessing |
| Valid Accounts | T1078 |
| Discovery | T1033 – Account Discovery |
| Discovery | T1082 – System Information Discovery |
| Defense Evasion | T1562.001 – Impair Defenses |
| Execution | T1059 – Command and Scripting Interpreter |
| Command & Control | T1071 – Application Layer Protocol |
| Command & Control | T1105 – Ingress Tool Transfer |
| Exfiltration | T1041 – Exfiltration Over C2 Channel |

---

# 🔄 Relationship to Other Project Phases

The attack simulation phase generated the telemetry used throughout the remainder of the project.

```text
Attack Simulation
        │
        ▼
Log Ingestion
        │
        ▼
Detection Engineering
        │
        ▼
Threat Hunting
        │
        ▼
Incident Response
        │
        ▼
Case Management
```

Every alert, dashboard, hunt, and investigation documented elsewhere in the repository originated from the attack activities performed during this phase.

---

# 🧠 Skills Demonstrated

This phase demonstrates practical experience with:

- Adversary Simulation
- Red Team Fundamentals
- Linux Administration
- Windows Administration
- Kali Linux
- Remote Desktop Protocol (RDP)
- Secure Shell (SSH)
- Mythic C2
- Malware Simulation
- Command & Control
- Endpoint Security
- Microsoft Defender
- Sysmon
- MITRE ATT&CK
- Security Testing
- Threat Emulation

---

# 🎯 Key Outcomes

By completing this phase, the following capabilities were demonstrated:

- Simulated external attacks against Windows and Linux systems
- Generated realistic endpoint and authentication telemetry
- Established a Command & Control session using Mythic
- Produced artifacts for detection engineering and threat hunting
- Validated Elastic Security detections
- Supported end-to-end SOC investigations

This phase provides the offensive simulation component of the MyDFIR SOC environment and serves as the foundation for the detection, investigation, and response activities documented throughout the remainder of the project.

---

# 🔗 Next Phase

The telemetry generated during these simulations was used to create detection rules, alerts, dashboards, and visualizations.

➡️ **Next Section**

```text
04-detection-engineering/
```

This section documents how the generated telemetry was transformed into actionable detections and SOC monitoring capabilities.
