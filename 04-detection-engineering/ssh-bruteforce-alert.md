# SSH Brute Force Alert Creation

## 📌 Objective
To create an SSH brute-force detection alert within Elasticsearch capable of identifying repeated failed authentication attempts against the Linux SSH server.

The detection focuses on:
- Failed SSH logins
- Source IP visibility
- Usernames targeted
- Geographic attack origin

---

# 🔍 Log Analysis Preparation

Reviewed available Linux authentication fields within Kibana Discover to identify useful telemetry for detection engineering.

---

# 🔹 Key Fields Identified

| Field | Purpose |
|---|---|
| `system.auth.ssh.event` | Authentication result |
| `user.name` | Targeted username |
| `source.ip` | Attacker IP address |
| `source.geo.country_name` | Geographic source location |

---

# 🔎 Failed Authentication Query

Filtered logs for failed SSH login attempts using KQL.

---

## 🔹 Example Query

kql
system.auth.ssh.event : "Failed"

---

## 📊 Saved Search Table

Created a saved table visualization containing:

- Failed authentication attempts
- Username field
- Source IP address
- Country name

Saved as:

SSH Failed Activity

---

## 🚨 Alert Rule Creation

Navigated to:

Alerts → Create Search Threshold Rule

# 🔹 Alert Configuration
Setting	                      Value
Rule Name              	MyDFIR-SSH Brute Force Activity - Tee
Detection Type	        Search Threshold
Threshold              	5 Failed Attempts
Time Window	            5 Minutes

## 🧪 Rule Testing

Reviewed and tested the Elasticsearch query to confirm:

Failed SSH events matched correctly
Alert threshold triggered as expected
Detection logic functioning properly
✅ Verification

Confirmed:

- SSH brute-force alert created successfully
- Detection query operational
- Threshold testing completed
- Failed authentication events triggering correctly

## 🔹 SSH Authentication Fields
![SSH Fields](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/ssh-fields.png)

---

## 🔹 SSH Query
![SSH Query](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/ssh-query.png)

---

## 🎯 Key Takeaways
- Created a functional SSH brute-force detection rule
- Leveraged Linux authentication telemetry
- Identified attacker IP addresses and usernames
- Established real-time alerting for suspicious authentication activity

This alert provides foundational SSH brute-force detection capabilities within the SOC environment.
