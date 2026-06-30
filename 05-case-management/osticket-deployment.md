# osTicket Deployment & Case Management Platform

## 📌 Objective

To deploy and configure osTicket as a centralized incident tracking and case management platform within the MyDFIR SOC environment.

The objective was to simulate real-world SOC workflows by enabling:

* Incident tracking
* Ticket creation
* Case assignment
* Investigation management
* Documentation of security events
* Security operations workflow management

This platform serves as the case management component of the SOC architecture.

---

# ☁️ Environment Overview

| Component          | Details             |
| ------------------ | ------------------- |
| Server Name        | MyDFIR-OS-Ticket    |
| Operating System   | Windows Server 2022 |
| Ticketing Platform | osTicket 1.18.4     |
| Web Server         | Apache (XAMPP)      |
| Database           | MySQL               |
| Hosting Platform   | Vultr               |

---

# 🖥️ Server Deployment

## 🔹 Windows Server Deployment

Deployed a new Windows Server 2022 instance in Vultr.

Configuration:

| Setting        | Value                       |
| -------------- | --------------------------- |
| Server Name    | MyDFIR-OS-Ticket            |
| Network        | VPC Enabled                 |
| Firewall Group | MyDFIR-SOC-Project Firewall |

The firewall group was attached to support future web application hosting.

---

# 🌐 XAMPP Installation

Downloaded and installed XAMPP.

Installation Path:

```text
C:\xampp
```

Verified:

* Apache installed successfully
* MySQL installed successfully
* Web server operational

---

# ⚙️ Apache Configuration

Modified Apache configuration settings.

Updated:

```text
Apache Domain Name
```

Changed from:

```text
127.0.0.1
localhost
```

To:

```text
155.138.156.62
```

Saved configuration successfully.

---

# 🗄️ phpMyAdmin Configuration

Created a backup:

```text
config.inc.backup.php
```

Modified:

```text
config.inc.php
```

Initially changed:

```text
127.0.0.1
```

To:

```text
155.138.156.62
```

This resulted in connectivity issues.

---

# ❌ Issue Encountered

phpMyAdmin failed to load correctly after changing the database host configuration.

The issue was caused by improper database host configuration.

---

# 🛠️ Troubleshooting & Resolution

Temporarily restored:

```text
127.0.0.1
```

Verified phpMyAdmin loaded successfully.

Modified MySQL user configuration and granted access permissions for the server IP address.

After updating user permissions, restored the public IP configuration and successfully connected.

---

# 🔥 Windows Firewall Configuration

Created inbound firewall rules allowing:

| Protocol | Port |
| -------- | ---- |
| TCP      | 80   |
| TCP      | 443  |

This enabled:

* HTTP access
* HTTPS access
* Web application connectivity

---

# 📦 osTicket Installation

Downloaded:

```text
osTicket 1.18.4
```

from:

```text
https://osticket.com
```

---

# 📁 Application Deployment

Extracted the osTicket package.

Created:

```text
C:\xampp\htdocs\osticket
```

Copied:

* scripts
* upload

folders into the deployment directory.

---

# 🌐 Installation Wizard

Navigated to:

```text
http://155.138.156.62/osticket/upload/
```

The installation wizard loaded successfully.

---

# ❌ Configuration File Error

During installation, osTicket reported:

```text
Configuration file missing
```

---

# 🛠️ Resolution

Renamed:

```text
include\ost-sampleconfig.php
```

To:

```text
include\ost-config.php
```

The installation wizard then proceeded successfully.

---

# 🗄️ Database Creation

A database was manually created within phpMyAdmin.

Database Name:

```text
myDFIR-InfSoc-Project-TD
```

Granted required privileges to the database user.

This resolved installation errors encountered during setup.

---

# ⚙️ osTicket Configuration

Configured:

| Setting       | Value                    |
| ------------- | ------------------------ |
| Helpdesk Name | MyDFIR-INF-Support       |
| Username      | myDFIR                   |
| Database      | myDFIR-InfSoc-Project-TD |

Installation completed successfully.

---

# 🔐 File Permission Configuration

Executed:

```powershell
icacls include\ost-config.php /reset
```

This restored appropriate permissions on the osTicket configuration file.

---

# 🌍 Access URLs

## Client Portal

```text
http://155.138.156.62/osticket/upload/
```

---

## Staff Control Panel

```text
http://155.138.156.62/osticket/upload/scp
```

---

# ✅ Verification

Confirmed:

* XAMPP operational
* Apache operational
* MySQL operational
* osTicket installed successfully
* Client portal accessible
* Staff control panel accessible
* Database connectivity functioning
* Case management platform operational

---

# 📸 Screenshots

## 🔹 XAMPP Installation

![XAMPP Installation](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/xampp-installation.png)

---

## 🔹 phpMyAdmin Access

![phpMyAdmin](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/phpmyadmin-success.png)

---

## 🔹 Client Portal

![Client Portal](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/osticket-client-portal.png)

---

## 🔹 Staff Control Panel

![Staff Control Panel](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/osticket-staff-panel.png)

---

# 🎯 Key Takeaways

* Successfully deployed a dedicated case management platform
* Installed and configured Apache, MySQL, and osTicket
* Implemented web server and database troubleshooting
* Created a centralized incident tracking solution
* Added a realistic SOC workflow component to the MyDFIR environment

This deployment completed the case management layer of the SOC architecture and provides a platform for documenting alerts, investigations, and incident response activities.
