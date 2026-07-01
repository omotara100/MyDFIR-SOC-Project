# Investigation Methodology – Mythic Apollo Process Execution

## Detection Summary

### Detection

**MyDFIR-Mythic-C2-Apollo**

### Severity

Critical

### Data Source

* Microsoft Sysmon
* Elastic Agent
* Elasticsearch
* Kibana

### MITRE ATT&CK

* T1059 – Command and Scripting Interpreter
* T1071 – Application Layer Protocol
* T1105 – Ingress Tool Transfer
* T1562.001 – Impair Defenses

---

# What Was Detected?

During the attack simulation, a custom executable (`svchost-tee.exe`) was launched on the Windows Server after being downloaded from the Mythic C2 infrastructure.

Although the executable had been renamed, Sysmon recorded the executable's original metadata, identifying the binary as **Apollo.exe**. This provided a reliable indicator for detecting execution of the Mythic agent regardless of the filename chosen by the attacker.

The alert was configured to trigger when either the original filename or the known SHA-256 hash of the payload was observed during a Sysmon Process Creation event (Event ID 1).

---

# Detection Logic

## Event Source

Sysmon Event ID 1 — Process Creation

## Query

```kql
event.code: 1 and (
winlog.event_data.Hashes: *8A3BE827182C18001C3CAA8DB1FE0808DBE5A341EB36FFEFA190CA555ACA8A13*
or
winlog.event_data.OriginalFileName: Apollo.exe
)
```

This detection identifies execution of the Apollo Mythic agent based on immutable file metadata rather than only the executable filename.

---

# Investigation Process

After the alert triggered, the following triage workflow was performed.

## Step 1 — Validate the Process

Reviewed:

* Image
* OriginalFileName
* SHA256 hash
* Parent Process
* Command Line
* Executing User

Objective:

Confirm the process matches the expected attack simulation.

---

## Step 2 — Review Parent Process

Reviewed:

* ParentImage
* ParentCommandLine

Objective:

Determine how the executable was launched.

Questions considered:

* Was it started from PowerShell?
* Was it started from Command Prompt?
* Was it launched manually?

---

## Step 3 — Validate Network Activity

Reviewed Sysmon Event ID 3 to determine whether the process initiated outbound communications.

Fields examined:

* Source IP
* Destination IP
* Destination Port
* Process Image

Objective:

Determine whether the process attempted to establish external communications consistent with command-and-control behaviour.

---

## Step 4 — Correlate Defender Activity

Reviewed Microsoft Defender operational logs (Event ID 5001).

Objective:

Determine whether endpoint protection had been disabled prior to payload execution.

This provided additional context supporting the attack timeline.

---

## Step 5 — Correlate with Mythic

Reviewed the Mythic Web UI.

Verified:

* Successful callback
* Active agent session
* Corresponding task execution

This confirmed that the detected process was associated with the simulated C2 infrastructure.

---

# True Positive

A true positive includes:

* Sysmon Event ID 1 showing execution of the payload
* Original filename recorded as Apollo.exe
* SHA-256 hash matching the known lab payload
* Outbound network communication from the same process
* Corresponding callback visible in Mythic
* Related attack activity generated during the lab exercise

---

# False Positive Considerations

Potential false positives include:

* Legitimate software sharing the same filename (unlikely)
* Testing performed by another analyst using the same lab payload
* Execution of archived malware samples in an isolated research environment

Using both the original filename and SHA-256 hash significantly reduces the likelihood of false positives.

---

# Investigation Outcome

The investigation confirmed successful execution of the Mythic Apollo agent during the controlled attack simulation.

Correlation across Sysmon process creation events, network telemetry, Microsoft Defender logs, and the Mythic management console demonstrated the complete attack chain from execution through command-and-control establishment.

---

# Lessons Learned

This investigation demonstrated the importance of correlating multiple telemetry sources rather than relying on a single alert.
