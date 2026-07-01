# Incident Investigation – Mythic Apollo Command & Control Activity

## 📌 Executive Summary

This investigation documents the detection and analysis of a simulated Command and Control (C2) attack using the Mythic framework against the Windows endpoint (`MyDFIR-WIN-Tee`) within the MyDFIR SOC environment.

The objective of this investigation was to validate the ability to detect post-exploitation activity by correlating endpoint telemetry, process creation events, network connections, Microsoft Defender logs, and Mythic callback activity.

The investigation demonstrates a typical SOC workflow for identifying malware execution and establishing whether an endpoint has successfully communicated with attacker infrastructure.

---

# Incident Information

| Field | Value |
|-------|-------|
| Incident ID | IR-003 |
| Incident Name | Mythic Apollo Command & Control |
| Severity | Critical |
| Status | Closed |
| Detection Source | Elastic Security Detection Rule |
| Affected Asset | MyDFIR-WIN-Tee |
| Operating System | Windows Server 2022 |

---

# Detection Summary

## Detection Rule

```text
MyDFIR-Mythic-C2-Apollo
```

Purpose:

Detect execution of the Mythic Apollo payload using Sysmon process creation events and immutable file metadata.

---

# Detection Logic

Sysmon Event ID 1 records detailed process creation telemetry, including process hashes and original file metadata.

The payload had been renamed to:

```text
svchost-tee.exe
```

However, Sysmon preserved:

```text
OriginalFileName = Apollo.exe
```

allowing reliable detection regardless of filename changes.

---

## Detection Query

```kql
event.code: 1 and (
winlog.event_data.Hashes: *8A3BE827182C18001C3CAA8DB1FE0808DBE5A341EB36FFEFA190CA555ACA8A13*
or
winlog.event_data.OriginalFileName: Apollo.exe
)
```

---

# MITRE ATT&CK Mapping

| Tactic | Technique |
|----------|----------|
| Defense Evasion | T1562.001 – Impair Defenses |
| Execution | T1059 – Command and Scripting Interpreter |
| Command & Control | T1071 – Application Layer Protocol |
| Command & Control | T1105 – Ingress Tool Transfer |
| Exfiltration | T1041 – Exfiltration Over C2 Channel |

---

# Investigation Timeline

| Time | Activity |
|------|----------|
| T0 | Payload downloaded to Windows endpoint |
| T1 | Payload executed |
| T2 | Sysmon Event ID 1 generated |
| T3 | Network connection initiated |
| T4 | Defender disabled |
| T5 | Mythic callback established |
| T6 | File download task executed |
| T7 | Investigation completed |

---

# Alert Validation

The investigation began after reviewing Sysmon events associated with the payload.

Searching for:

```text
svchost-tee.exe
```

identified multiple Sysmon events related to payload execution.

Although the executable name had been modified, Sysmon retained the original file metadata, revealing:

```text
OriginalFileName = Apollo.exe
```

This confirmed the payload identity.

---

# Investigation Methodology

## Step 1 — Validate Process Creation

Reviewed Sysmon Event ID 1.

Fields examined:

| Field | Purpose |
|---------|---------|
| Image | Executed process |
| OriginalFileName | Original executable name |
| Hashes | SHA256 verification |
| User | Executing account |
| ParentImage | Parent process |
| ParentCommandLine | Launch source |
| CommandLine | Execution command |
| CurrentDirectory | Execution path |
| ProcessGuid | Process correlation |

Objective:

Determine whether the process matched the expected Mythic payload.

---

## Step 2 — Validate Malware Identity

Compared:

- OriginalFileName
- SHA256 hash

Observed:

Original filename remained:

```text
Apollo.exe
```

The SHA256 hash matched the payload generated during the attack simulation.

This confirmed the process was the expected Mythic agent.

---

## Step 3 — Investigate Network Activity

Reviewed Sysmon Event ID 3.

Fields examined:

| Field |
|--------|
| Image |
| SourceIp |
| DestinationIp |
| DestinationPort |

Objective:

Determine whether the process attempted outbound communication.

Observed:

- Outbound connection initiated
- Destination matched Mythic infrastructure

---

## Step 4 — Review Microsoft Defender Activity

Reviewed Microsoft Defender Operational logs.

Focused on:

Event ID:

```text
5001
```

Description:

```text
Microsoft Defender Antivirus Real-time Protection was disabled.
```

Objective:

Determine whether endpoint protection had been disabled prior to payload execution.

This activity aligned with the planned attack simulation.

---

## Step 5 — Validate Command & Control

Reviewed the Mythic Web UI.

Confirmed:

- Active callback
- Successful agent registration
- Command execution capability

This established successful communication between the endpoint and the Mythic server.

---

## Step 6 — Validate Exfiltration Activity

Reviewed Mythic task history.

Observed successful retrieval of the test document from the Windows endpoint.

This confirmed completion of the simulated attack lifecycle.

---

# Evidence Collected

Evidence reviewed included:

| Evidence | Purpose |
|----------|---------|
| Sysmon Event ID 1 | Process execution |
| Sysmon Event ID 3 | Network communication |
| Defender Event ID 5001 | Security control changes |
| SHA256 Hash | Payload validation |
| OriginalFileName | Malware identification |
| Mythic Callback | C2 validation |
| Download Task | Exfiltration verification |

---

# True Positive Analysis

The alert was classified as a **True Positive** because:

- Sysmon recorded process creation.
- OriginalFileName identified Apollo.exe.
- SHA256 matched the generated payload.
- Outbound communication was established.
- Microsoft Defender was disabled before execution.
- Mythic successfully received a callback.
- Command execution succeeded.
- Simulated file retrieval completed.

Multiple independent telemetry sources confirmed the attack.

---

# False Positive Considerations

Potential false positives could include:

- Malware analysis in an isolated sandbox.
- Internal security testing.
- Authorized red team exercises.

In this environment, the activity directly correlated with the controlled Mythic simulation and was therefore expected.

---

# Findings

The investigation confirmed:

- Successful payload execution.
- Successful outbound communication.
- Successful C2 registration.
- Defender tampering prior to execution.
- Successful command execution.
- Successful file retrieval through Mythic.

The complete attack lifecycle was observable using Elastic Security.

---

# Analyst Assessment

This investigation demonstrates the importance of correlating multiple telemetry sources.

A single process execution event is rarely sufficient to determine compromise.

By combining:

- Process creation
- Network connections
- Endpoint protection status
- Callback activity
- Threat intelligence

the investigation reached a high-confidence conclusion.

---

# Lessons Learned

This investigation highlighted several important detection engineering concepts:

- Original file metadata is often more reliable than executable names.
- SHA256 hashes provide strong indicators for known malware.
- Sysmon Event ID 1 offers extensive endpoint visibility.
- Event ID 3 is valuable for identifying outbound C2 communications.
- Defender operational logs provide useful context during malware investigations.
- Correlation across multiple telemetry sources significantly improves analyst confidence.

---

# Skills Demonstrated

- Malware Investigation
- Endpoint Detection
- Sysmon Analysis
- Process Creation Analysis
- Network Connection Analysis
- Threat Hunting
- Detection Engineering
- KQL Query Development
- MITRE ATT&CK Mapping
- SOC Investigation Workflow
- Incident Documentation

---

# Investigation Outcome

**Classification:** True Positive

**Impact:** High

**Compromise Confirmed:** Yes (Controlled Lab Simulation)

**Root Cause:** Execution of the Mythic Apollo agent during a controlled attack simulation.

The investigation successfully demonstrated end-to-end detection and analysis of a simulated command-and-control attack using Elastic Security, Sysmon, Microsoft Defender telemetry, and Mythic C2.

---

# 📸 Investigation Evidence

## 🔹 Attack Lifecycle Diagram
![Attack Diagram](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/attacker-diagram.png)

---

## 🔹 Mythic Payload Investigation
![Payload Investigation](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/svchost-tee-investigation.png)

---

## 🔹 Apollo Process Creation
![Apollo Process](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/apollo-process-create.png)

---

## 🔹 Apollo Detection Query
![Apollo Query](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/apollo-detection-query.png)

---

## 🔹 Mythic Detection Rule
![Mythic Rule](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/mythic-apollo-rule.png)

---

## 🔹 Process Creation Dashboard
![Process Dashboard](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/process-created-dashboard.png)

---

## 🔹 Outbound Network Activity
![Network Dashboard](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/process-created-initiated-network.png)

---

## 🔹 Microsoft Defender Disabled
![Defender Disabled](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/microsoft-defender-disabled.png)

---

## 🔹 Mythic Callback
![Mythic Callback](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/mythic-callback.png)

---

## 🔹 Retrieved File
![Retrieved File](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/password-file-preview.png)
