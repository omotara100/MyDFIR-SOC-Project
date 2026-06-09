# Mythic Agent Deployment, Command & Control, and Data Exfiltration

## 📌 Objective

To simulate post-exploitation activity using the Mythic C2 framework and understand how command-and-control infrastructure operates in modern attack scenarios.

This exercise focused on:

- Defense evasion
- Agent deployment
- Command and Control (C2)
- Callback communications
- Data exfiltration
- Detection opportunities

---

# 🏗️ Environment Overview

| Component | Purpose |
|------------|------------|
| Mythic C2 Server | Command & Control platform |
| Windows Server 2022 | Victim endpoint |
| Kali Linux | Attacker workstation |
| Elastic Stack | Monitoring platform |

---

# 🔍 Phase 3 – Defense Evasion

Prior to agent deployment, endpoint protection settings were modified to simulate a weakened security posture.

Objective:

- Demonstrate defense evasion activity
- Generate Defender telemetry
- Create detection opportunities

---

# ⚙️ Phase 4 – Agent Deployment

## Apollo Agent Installation

The Apollo Mythic agent was installed within the Mythic platform.

The Apollo agent was selected because it supports:

- HTTP
- HTTPS
- TCP
- SMB

communication profiles.

---

## C2 Profile Installation

An HTTP C2 profile was installed and configured.

The profile was used to:

- Receive callbacks
- Issue commands
- Transfer files
- Simulate attacker communications

---

## Payload Generation

A Windows payload was generated through the Mythic Web UI.

Configuration included:

- Windows target platform
- HTTP callback profile
- Custom payload naming
- Default command set

---

# 🌐 Payload Delivery

The payload was transferred to the Windows endpoint and executed.

Verification included:

- Process execution validation
- Network communication checks
- Callback monitoring

---

# 📡 Phase 5 – Command & Control

Following execution, the agent successfully established communication with the Mythic server.

Activities included:

- Agent registration
- Callback creation
- Command execution
- Session management

---

## Communication Verification

Network activity was validated using:

```text
netstat
```

Observed:

- Initial connection attempts
- Established C2 communications
- Active callback sessions

---

# 📂 Phase 6 – Data Exfiltration

A test document was downloaded from the compromised endpoint using Mythic tasking functionality.

Objectives:

- Simulate data theft
- Demonstrate attacker objectives
- Generate telemetry for detection

---

# 🧠 MITRE ATT&CK Mapping

| Tactic | Technique |
|----------|----------|
| Defense Evasion | T1562.001 Impair Defenses |
| Execution | T1059 Command Execution |
| Command & Control | T1071 Application Layer Protocol |
| Command & Control | T1105 Ingress Tool Transfer |
| Exfiltration | T1041 Exfiltration Over C2 Channel |

---

# ✅ Verification

Confirmed:

- Apollo agent installed successfully
- HTTP C2 profile operational
- Payload generated successfully
- Callback established
- Command execution functional
- File transfer successful
- Exfiltration workflow demonstrated

---

# 📸 Screenshots

## 🔹 Apollo Agent Installed
![Apollo Agent Installed](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/apollo-agent-installed.png)

---

## 🔹 HTTP C2 Profile
![HTTP C2 Profile](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/http-c2-profile-installed.png)

---

## 🔹 Payload Creation
![Payload Creation](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/payload-creation.png)

---

## 🔹 Payload Running
![Payload Running](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/payload-running-taskmanager.png)

---

## 🔹 Network Communication Established
![Network Communication](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/netstat-established.png)

---

## 🔹 Mythic Callback
![Mythic Callback](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/mythic-callback.png)

---

## 🔹 File Download Task
![Apollo Download Command](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/apollo-download-command.png)

---

## 🔹 Retrieved File Preview
![Password File Preview](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/password-file-preview.png)

---

# 🎯 Key Takeaways

- Successfully deployed Mythic C2 infrastructure
- Installed and configured Apollo agent
- Established command-and-control communications
- Simulated post-exploitation activities
- Demonstrated controlled data exfiltration
- Generated realistic telemetry for SOC investigations

This exercise completed the full attack lifecycle from initial access through command-and-control and data exfiltration, providing realistic adversary behavior for detection engineering and DFIR analysis.
