# Incident Investigation – RDP Brute Force Attack

## 📌 Executive Summary

This investigation documents a simulated Remote Desktop Protocol (RDP) brute-force attack against the Windows Server (`MyDFIR-WIN-Tee`) within the MyDFIR SOC environment.

The objective was to validate the organization's ability to detect, investigate, and respond to unauthorized authentication attempts targeting exposed RDP services.

This investigation followed a structured SOC triage process using:

- Windows Security Logs
- Sysmon
- Elastic Agent
- Kibana Discover
- Elastic Security Detection Rules
- Authentication Dashboards

---

# Incident Information

| Field | Value |
|-------|-------|
| Incident ID | IR-002 |
| Incident Name | Windows RDP Brute Force Attempt |
| Severity | Medium |
| Status | Closed |
| Detection Source | Elastic Security Detection Rule |
| Affected Asset | MyDFIR-WIN-Tee |
| Operating System | Windows Server 2022 |

---

# Detection Summary

## Detection Rule

```text
MyDFIR-RDP-Brute-Force-Attempt-Tee
```

Purpose:

Detect repeated failed RDP authentication attempts against the Windows Administrator account.

---

## Detection Logic

### Detection Query

```kql
event.code: 4625
and
agent.name: "MYDFIR-WINTee"
and
user.name: "Administrator"
```

---

# MITRE ATT&CK Mapping

| Tactic | Technique |
|---------|-----------|
| Initial Access | T1110 – Brute Force |
| Credential Access | T1110.001 – Password Guessing |
| Initial Access | T1078 – Valid Accounts |

---

# Investigation Timeline

| Time | Activity |
|------|----------|
| T0 | Failed RDP authentication attempts generated |
| T1 | Detection rule triggered |
| T2 | Alert triaged |
| T3 | Windows Security logs reviewed |
| T4 | Source IP correlated |
| T5 | Successful authentication investigated |
| T6 | Incident documented |

---

# Alert Validation

The investigation began by reviewing the Elastic Security alert.

The alert identified repeated Windows authentication failures against the Administrator account.

Initial observations included:

- Multiple Event ID 4625 records
- Repeated authentication failures
- External source IP address
- Administrator account targeted

---

# Investigation Methodology

## Step 1 — Review Failed Authentication Events

Opened Kibana Discover.

Executed:

```kql
event.code: 4625
```

Confirmed:

- Failed authentication events
- Username
- Source IP
- Authentication timestamps

---

## Step 2 — Validate Target Account

Reviewed:

```text
user.name
```

Observed:

```text
Administrator
```

This confirmed the attack targeted the built-in Windows administrative account.

---

## Step 3 — Review Source Information

Examined:

- source.ip
- source.geo.country_name

Objective:

Determine:

- Origin of authentication attempts
- Geographic source
- Repeat activity

---

## Step 4 — Investigate Successful Logins

To determine whether the attacker eventually authenticated successfully, reviewed Windows successful authentication events.

Query:

```kql
event.code: 4624 and
(
winlog.event_data.LogonType: 10
or
winlog.event_data.LogonType: 7
)
```

---

# Logon Type Analysis

| Logon Type | Description |
|------------|-------------|
| 10 | Remote Interactive (RDP) |
| 7 | Workstation Unlock |

The successful authentication events were correlated with the planned lab activity.

---

## Step 5 — Correlate Timeline

Compared:

- Failed authentication events
- Successful authentication events
- Alert timestamps
- Dashboard activity

This established the complete authentication timeline.

---

# Evidence Collected

Evidence reviewed included:

| Evidence | Purpose |
|----------|---------|
| Event ID 4625 | Failed logins |
| Event ID 4624 | Successful logins |
| Username | Target account |
| Source IP | Attacker identification |
| Country | Geographic attribution |
| Dashboard | Authentication visualization |

---

# True Positive Analysis

The alert was classified as a **True Positive** because:

- Multiple failed RDP authentication attempts occurred.
- The Administrator account was targeted.
- Authentication events matched the detection logic.
- Activity originated from an external source.
- Events correlated with the controlled attack simulation.

---

# False Positive Considerations

Potential false positives include:

- Administrator repeatedly entering an incorrect password.
- Remote administration from trusted personnel.
- Password synchronization issues.

Correlation with the attack timeline confirmed the activity was expected and intentionally generated.

---

# Findings

The investigation determined:

- Repeated failed RDP authentication attempts occurred.
- Windows Security Event ID 4625 accurately recorded the failures.
- Event ID 4624 recorded successful authentication after valid credentials were used.
- Detection rules successfully generated alerts.
- Dashboards accurately reflected authentication activity.

---

# Analyst Assessment

The investigation demonstrated successful detection of a credential attack targeting RDP.

Authentication telemetry clearly distinguished between:

- Failed login attempts
- Successful authentication
- Remote interactive logons

The attack was contained within the controlled lab environment.

---

# Lessons Learned

This investigation demonstrated:

- Windows Event ID 4625 is essential for detecting failed logins.
- Event ID 4624 should always be reviewed to determine whether the attack ultimately succeeded.
- Correlating failed and successful authentication provides a complete picture of the attack lifecycle.
- Authentication dashboards significantly reduce investigation time.

---

# Skills Demonstrated

- Windows Event Log Analysis
- Authentication Investigation
- Kibana Discover
- Elastic Security
- Detection Rule Validation
- Event Correlation
- Incident Triage
- Threat Detection
- MITRE ATT&CK Mapping

---

# Investigation Outcome

**Classification:** True Positive

**Impact:** Medium

**Compromise Confirmed:** Controlled Lab Access

**Root Cause:** Simulated RDP brute-force attack against the Windows Server.

The investigation confirmed that the Windows authentication telemetry, Elastic Security detections, and dashboards accurately identified both failed and successful RDP authentication events throughout the simulated attack.

---

# 📸 Investigation Evidence

## 🔹 Windows Event ID 4625
![Windows Event 4625](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/windows-event-4625.png)

---

## 🔹 RDP Failed Activity Query
![RDP Failed Query](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/rdp-failed-query.png)

---

## 🔹 RDP Failed Dashboard
![RDP Failed Dashboard](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/rdp-failed-dashboard.png)

---

## 🔹 RDP Successful Authentication Dashboard
![RDP Successful Dashboard](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/rdp-success-dashboard.png)

---

## 🔹 RDP Failed Authentication Table
![RDP Failed Table](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/rdp-failed-auth-table.png)

---

## 🔹 RDP Successful Authentication Table
![RDP Successful Table](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/rdp-success-auth-table.png)

---

## 🔹 Elastic Security Detection Rule
![RDP Detection Rule](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/rdp-siem-rule.png)
