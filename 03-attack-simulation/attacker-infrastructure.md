# Attacker Infrastructure & Attack Lifecycle

## 📌 Objective

To design and document the attacker infrastructure used to simulate realistic adversary behavior against the Windows endpoint within the SOC/DFIR environment.

The attack scenarios support:
- RDP brute-force attacks
- Initial access simulation
- Malware execution
- Command and Control (C2) activity
- Data exfiltration scenarios
- Detection engineering validation
- Threat hunting investigations

---

## 🏗️ Attack Lifecycle Diagram

![Attacker Diagram](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/attacker-diagram.png)

## Phase 1 – Initial Access

The attacker system (Kali Linux) targets the public-facing Windows Server using RDP authentication attempts.

Objectives:
- Password guessing
- Credential attacks
- Initial access simulation

---

## Phase 2 – Successful Authentication

After obtaining valid credentials, the attacker gains interactive access to the Windows server.

Objectives:
- Establish user access
- Simulate compromised credentials
- Generate authentication telemetry

---

## Phase 3 – Discovery & Defense Evasion

The attacker performs host reconnaissance and evaluates security controls.

Activities:
- System discovery
- User enumeration
- Security tool identification
- Windows Defender inspection

---

## Phase 4 – Malware Execution

A Mythic agent is executed on the Windows endpoint.

Objectives:
- Establish attacker foothold
- Execute payloads
- Generate endpoint telemetry

---

## Phase 5 – Command & Control

The compromised endpoint communicates with the Mythic C2 server.

Activities:
- Beaconing
- Command execution
- Remote tasking

---

## Phase 6 – Data Exfiltration

Simulated sensitive data is collected and transmitted through the C2 channel.

Objectives:
- Demonstrate attacker objectives
- Generate detection opportunities
- Support DFIR investigations
