# Windows RDP Brute Force Detection & SIEM Alerting

## 📌 Objective
To monitor Windows authentication telemetry and create brute-force detection alerts for failed RDP authentication attempts within the SOC/DFIR environment.

The objective was to:
- Detect failed Windows logins
- Monitor RDP authentication activity
- Create threshold-based alerts
- Build SIEM detection rules
- Improve visibility into brute-force attacks

---

# 🪟 Windows Authentication Monitoring

Opened Kibana Discover and filtered logs for the Windows endpoint:

agent.name : "MyDFIR-WIN-Tee"

---

## 🔍 Failed Authentication Analysis

Reviewed Windows authentication events and identified:

Event ID	        Description
4625	         Failed Windows Logon Attempt

---

# 🔹 Authentication Query

Searched for failed authentication events using:

event.code : 4625

Observed:

- Failed RDP authentication attempts
- Source IP addresses
- Username activity
- Windows authentication telemetry

---

## 📊 Authentication Activity Table

Created a table including the following fields:

Field             	    Purpose
Failed Attempts       	Authentication monitoring
source.ip	              Attacker IP address
user.name	              Targeted account
event.code	            Authentication event ID

Saved the query as:

RDP Failed Activity Query

---

## 🧪 RDP Attack Testing

Performed test RDP login attempts and reviewed generated events.

Observed:

- Failed logon activity
- Logon Type 3 events
- Authentication telemetry generated successfully

## 🚨 Search Threshold Alert Rule

Created a threshold-based alert rule.

Navigated to:

Alerts → Create Search Threshold Rule

---

# 🔹 Rule Configuration
Setting            	Value
Rule Name	          MyDFIR-RDP Brute Force Activity-Tee
Detection Type	    Search Threshold Rule

This alert generated notifications based on repeated failed authentication attempts.

---

# ⚠️ Limitation Identified

Observed that standard threshold alerts provided limited investigation context and alert enrichment.

This led to exploring SIEM Detection Rules within Elastic Security.

---

## 🛡️ Elastic Security Detection Rules

Navigated to:

Security → Rules → Detection Rules

Selected:

Create Rule → Manual Create Rule → Threshold Rule

---

## 🔐 SSH Brute Force SIEM Rule

Created an advanced SIEM detection rule for SSH brute-force attempts.

---

# 🔹 SSH Rule Query
system.auth.ssh.event : * and agent.name: "MYDFIR-Linux-Tee" and system.auth.ssh.event: "Failed" and user.name: "root"

---

# 🔹 SSH Rule Details
Setting           	Value
Rule Name	          MyDFIR-SSH-Brute-Force-Attempt-Tee
Severity	          Medium

---
# 🔹 Description

This rule detects failed authentication attempts toward the root account via SSH.

---

## 🪟 RDP Brute Force SIEM Rule

Created a second SIEM detection rule for Windows RDP brute-force activity.

---

# 🔹 RDP Rule Query
event.code: 4625 and agent.name: "MYDFIR-WINTee" and user.name: "Administrator"

---

# 🔹 RDP Rule Details
Setting                   	Value
Rule Name                 	MyDFIR-RDP-Brute-Force-Attempt-Tee
Severity                   	Medium

---

# 🔹 Description

This rule detects failed authentication attempts toward the Administrator account via RDP.

---

## ✅ Verification

Confirmed:

- Failed Windows authentication events detected successfully
- Threshold alerts operational
- SIEM Detection Rules created successfully
- SSH and RDP brute-force monitoring active
- Rules visible within Elastic Security Detection Rules

---
## 🔹 Windows Event ID 4625
![Windows Event ID 4625](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/windows-event-4625.png)

---

## 🔹 RDP Failed Activity Query
![RDP Failed Activity Query](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/rdp-failed-query.png)

---

## 🔹 RDP Attempt Events
![RDP Attempt Events](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/rdp-attempt-events.png)

---

## 🔹 Threshold Alert Rule
![Threshold Alert Rule](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/threshold-alert-rule.png)

---

## 🔹 Stack Management Alerts
![Stack Management Alerts](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/stack-management-alerts.png)

---

## 🔹 SSH SIEM Detection Rule
![SSH SIEM Rule](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/ssh-siem-rule.png)

---

## 🔹 RDP SIEM Detection Rule
![RDP SIEM Rule](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/rdp-siem-rule.png)

---

## 🔹 Elastic Security Detection Rules
![Elastic Detection Rules](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/elastic-detection-rules.png)


---

## 🔐 Security Value

These detections improve:

- Windows authentication monitoring
- SSH brute-force visibility
- RDP attack detection
- Account-focused monitoring
- SOC investigation capability
- SIEM alert enrichment

  ---
  
## 🎯 Key Takeaways
- Successfully created Windows RDP brute-force detection alerts
- Monitored failed authentication attempts using Event ID 4625
- Built SIEM threshold detection rules for SSH and RDP activity
- Improved detection quality using Elastic Security Detection Rules
- Enhanced authentication monitoring across Linux and Windows environments

This phase significantly expanded the SOC detection engineering capability within the lab environment and introduced SIEM-focused brute-force monitoring workflows.
