# 05 – Case Management

## 📌 Overview

This section documents the deployment and implementation of a case management platform within the **MyDFIR-SOC-Project** using **osTicket**.

A Security Operations Center (SOC) does not end with detection. Once an alert is generated and investigated, it must be documented, assigned, tracked, and resolved. To simulate this operational workflow, an osTicket help desk platform was deployed as the project's incident management system.

This phase demonstrates how security investigations transition into documented incidents that can be tracked through their lifecycle, providing a realistic SOC environment beyond detection engineering.

---

# 🎯 Objectives

The objectives of this phase were to:

- Deploy a dedicated case management platform
- Configure a Windows-based web server using XAMPP
- Install and configure osTicket
- Configure Apache and MySQL services
- Build an incident tracking platform
- Support investigation documentation
- Simulate enterprise SOC workflows

---

# 🏗️ Environment

| Component | Details |
|------------|----------|
| Platform | osTicket 1.18.4 |
| Operating System | Windows Server 2022 |
| Web Server | Apache (XAMPP) |
| Database | MySQL |
| Cloud Provider | Vultr |
| Server Name | MyDFIR-OS-Ticket |

---

# 🛠 Components Configured

The following infrastructure components were deployed and configured.

## Windows Server

- Windows Server 2022
- Public IP Address
- Firewall Group
- Remote Desktop Access

---

## XAMPP

Installed and configured:

- Apache
- MySQL
- PHP
- phpMyAdmin

---

## Database

Configured:

- MySQL
- Database creation
- User privileges
- Database connectivity

---

## osTicket

Configured:

- Help Desk
- Client Portal
- Staff Control Panel
- Administrator Account
- Incident Database

---

# 📂 Documentation

## osTicket Deployment

The deployment guide includes:

- Windows Server deployment
- XAMPP installation
- Apache configuration
- MySQL configuration
- phpMyAdmin troubleshooting
- osTicket installation
- Database configuration
- File permission configuration
- Firewall configuration
- Validation testing

📄 **File**

```text
osticket-deployment.md
```

---

# 🔄 Incident Management Workflow

The case management platform supports the following SOC workflow.

```text
Security Alert
       │
       ▼
Alert Validation
       │
       ▼
Investigation
       │
       ▼
Case Creation
       │
       ▼
Evidence Collection
       │
       ▼
Documentation
       │
       ▼
Resolution
       │
       ▼
Case Closure
```

---

# 📊 Case Management Capabilities

The deployed platform supports:

- Incident documentation
- Ticket assignment
- Investigation tracking
- Analyst collaboration
- Resolution tracking
- Historical case records

---

# 🔐 SOC Integration

The osTicket platform integrates with the previous project phases.

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

Each alert investigated during the project can now be documented within a structured ticketing system, closely reflecting enterprise SOC operations.

---

# 📋 Example Incident Types

The platform is intended to document investigations such as:

- SSH Brute Force Attempts
- Windows RDP Brute Force Attempts
- Mythic Apollo Execution
- Command and Control Activity
- Microsoft Defender Tampering
- Suspicious PowerShell Execution
- Suspicious Network Connections

---

# 🧠 Skills Demonstrated

This phase demonstrates practical experience with:

- Incident Handling
- Case Management
- Security Operations Workflow
- Ticket Lifecycle Management
- Windows Server Administration
- Apache Administration
- MySQL Administration
- Web Application Deployment
- XAMPP Configuration
- Firewall Configuration
- Documentation & Reporting

---

# 📈 Security Value

Implementing a dedicated case management platform provides:

- Centralized incident documentation
- Consistent investigation workflow
- Improved evidence tracking
- Better analyst collaboration
- Historical investigation records
- Repeatable SOC processes

---

# 🎯 Key Outcomes

By completing this phase, the following capabilities were implemented:

- Deployed a production-style ticketing platform
- Configured a web server and database backend
- Installed and secured osTicket
- Validated client and analyst access
- Established a structured incident tracking workflow
- Completed the final operational component of the MyDFIR SOC environment

This phase completes the operational lifecycle of the project by providing a platform to document, manage, and track security incidents from initial detection through investigation and final resolution.

---

# 🔗 Related Project Sections

| Phase | Purpose |
|---------|----------|
| **01-lab-setup** | Infrastructure deployment |
| **02-log-ingestion** | Centralized telemetry collection |
| **03-attack-simulation** | Adversary simulation |
| **04-detection-engineering** | Alert creation and dashboards |
| **05-threat-hunting** | Proactive threat investigations |
| **06-incident-response** | Alert triage and investigation |
| **07-case-management** *(Optional Future Expansion)* | Case tracking, metrics, SLAs, and reporting |

---

# 🚀 Next Steps

Future enhancements planned for the case management platform include:

- Creating incident tickets directly from completed investigations
- Defining incident severity classifications
- Building analyst playbooks
- Creating standardized response templates
- Measuring response metrics (MTTD/MTTR)
- Developing investigation reports linked to individual tickets

These enhancements will further align the project with enterprise SOC operations and incident management best practices.
