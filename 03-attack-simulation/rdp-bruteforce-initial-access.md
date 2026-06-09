# RDP Brute Force Simulation & Initial Access

## 📌 Objective

To simulate an external attacker attempting to gain unauthorized access to a public-facing Windows Server through Remote Desktop Protocol (RDP).

The purpose of this exercise was to:

- Generate authentication telemetry
- Validate Windows logging visibility
- Test brute-force detections
- Produce realistic SOC investigation data
- Simulate the Initial Access phase of the attack lifecycle

---

# 🏗️ Attack Scenario

The environment consisted of:

| Component | Purpose |
|------------|------------|
| Kali Linux | Attacker system |
| Windows Server 2022 | Target system |
| Elastic Stack | Monitoring platform |
| Sysmon | Endpoint telemetry |
| Windows Defender | Security monitoring |

---

# 🔍 Phase 1 – Initial Access

The attacker system attempted authentication against the public-facing Windows Server.

Objectives:

- Generate failed authentication attempts
- Trigger detection rules
- Produce Event ID 4625 telemetry
- Validate SOC monitoring visibility

---

# 📊 Authentication Monitoring

Authentication activity was observed through:

- Windows Security Logs
- Elastic Agent
- Elasticsearch
- Kibana Discover
- Detection Rules

---

# 🔐 Successful Authentication

After valid credentials were obtained, a successful RDP session was established to the target system.

Objectives:

- Simulate compromised credentials
- Generate successful login telemetry
- Produce Event ID 4624 events
- Continue attack lifecycle activities

---

# 🔍 Phase 2 – Discovery

Following successful authentication, discovery activities were performed to gather host information.

Activities included:

- User identification
- Network configuration review
- Local account enumeration
- Host reconnaissance

Examples:

```text
whoami
ipconfig
net user
```

---

# 🧠 MITRE ATT&CK Mapping

| Tactic | Technique |
|----------|----------|
| Initial Access | T1110 - Brute Force |
| Initial Access | T1078 - Valid Accounts |
| Discovery | T1033 - Account Discovery |
| Discovery | T1082 - System Information Discovery |

---

# ✅ Verification

Confirmed:

- Failed authentication events generated
- Successful authentication events generated
- Event ID 4625 visibility confirmed
- Event ID 4624 visibility confirmed
- Detection rules triggered successfully
- Telemetry visible within Elasticsearch

---

# 📸 Screenshots

## 🔹 Attack Lifecycle Diagram
![Attack Diagram](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/attacker-diagram.png)

---

## 🔹 Discovery Commands
![Discovery Commands](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/windows-discovery-commands.png)

---

# 🎯 Key Takeaways

- Successfully simulated external authentication attacks
- Generated realistic Windows authentication telemetry
- Validated SOC monitoring workflows
- Produced data for detection engineering exercises
- Established initial access required for subsequent attack phases

This exercise demonstrated how authentication attacks can be detected, monitored, and investigated within a SOC environment.
