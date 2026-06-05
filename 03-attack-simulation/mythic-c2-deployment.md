# Mythic C2 Server Deployment

## 📌 Objective

To deploy a Mythic Command and Control (C2) server and gain hands-on experience with adversary infrastructure commonly used during red team operations and post-exploitation activities.

The Mythic platform will be used to simulate:

- Initial access
- Malware execution
- Command and Control (C2)
- Defense evasion
- Post-exploitation activities
- Data exfiltration

This infrastructure will generate realistic attacker telemetry for SOC monitoring, detection engineering, threat hunting, and DFIR investigations.

---

# ☁️ Environment Overview

| Component | Details |
|---|---|
| Server Name | `MyDFIR-Mythic` |
| Operating System | Ubuntu 22.04 |
| Platform | Mythic C2 |
| Purpose | Adversary Simulation Infrastructure |
| Public IP Address | `149.248.63.128` |

---

# 🖥️ Server Deployment

## 🔹 Deployment Steps

1. Deployed a new Ubuntu 22.04 server in Vultr
2. Assigned the hostname:

```text
MyDFIR-Mythic
```

3. Connected remotely using SSH

---

# 🔄 System Preparation

Updated the operating system:

```bash
apt update && apt upgrade -y
```

---

# 📦 Required Dependencies

Installed Docker Compose:

```bash
apt install docker-compose -y
```

Installed Make:

```bash
apt install make -y
```

---

# 📥 Mythic Installation

Cloned the Mythic repository:

```bash
git clone https://github.com/its-a-feature/Mythic
```

Verified repository download:

```bash
ls
```

---

# ⚙️ Docker Configuration

Executed the Mythic Docker installation script:

```bash
./install_docker_ubuntu.sh
```

---

# ❌ Issue Encountered

While building Mythic, the following error occurred:

```text
Cannot connect to the Docker daemon
```

This prevented the Mythic containers from starting successfully.

---

# 🛠️ Troubleshooting & Resolution

Verified Docker service status:

```bash
systemctl status docker
```

Observed:
- Docker service not running

Restarted Docker:

```bash
systemctl restart docker
```

Verified Docker status again:

```bash
systemctl status docker
```

Confirmed:
- Docker service active and running

---

# 🏗️ Mythic Build Process

Built the Mythic platform:

```bash
make
```

The build completed successfully after Docker was restored.

---

# ▶️ Starting Mythic

Started Mythic using:

```bash
./mythic-cli start
```

Confirmed:
- Mythic services started successfully
- Containers operational
- Web interface available

---

# 🔥 Firewall Configuration

To limit communication only to approved systems, a dedicated firewall group was created.

---

## 🔹 Firewall Group

Created:

```text
MyDFIR-Mythic-Firewall
```

---

## 🔹 Rule 1 – Administrator Access

| Setting | Value |
|---|---|
| Protocol | TCP |
| Port Range | 1-65535 |
| Source | Personal Public IP |

Purpose:
- Administrative access
- Mythic management
- Web interface access

---

## 🔹 Rule 2 – Windows Endpoint Access

| Setting | Value |
|---|---|
| Source | 149.248.56.62/32 |

Purpose:
- Allow communication from the Windows Server endpoint

---

## 🔹 Rule 3 – Linux Endpoint Access

Added the Linux SSH server public IP address.

Purpose:
- Future testing and agent communication scenarios

---

## 🔹 Firewall Assignment

Applied the firewall group to:

```text
MyDFIR-Mythic
```

---

# 🌐 Accessing Mythic

Opened the Mythic web interface:

```text
http://149.248.63.128:7443
```

Successfully accessed:
- Mythic login page
- Mythic administrative dashboard

---

# ✅ Verification

Confirmed:

- Mythic server deployed successfully
- Docker environment operational
- Mythic containers running
- Firewall restrictions applied
- Web interface accessible
- Mythic dashboard operational

---

## 🔹 Mythic Login Page
![Mythic Login](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/mythic-login-page.png)

---

## 🔹 Mythic Dashboard
![Mythic Dashboard](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/mythic-dashboard.png)

---

# 🔐 Security Considerations

The following security controls were implemented:

- Dedicated firewall group
- Restricted inbound communication
- Endpoint-specific access controls
- Controlled administrative access
- Segmentation of attacker infrastructure

---

# 🎯 Key Takeaways

- Successfully deployed Mythic C2 infrastructure
- Installed and configured Docker-based services
- Troubleshot Docker daemon issues
- Restricted communications using firewall controls
- Established an attacker simulation platform for future post-exploitation exercises

This deployment established the adversary infrastructure required for command-and-control simulations, malware execution testing, and threat hunting exercises within the SOC/DFIR environment.
