# Kibana Deployment & Configuration

## 📌 Objective
To deploy and configure Kibana for visualization, monitoring, and analysis of logs collected within the SOC/DFIR lab environment.

---

## ☁️ Environment Details

### 🔹 Server Information
- Hosted on Vultr Cloud
- Installed on the Elasticsearch server instance
- Operating System: Ubuntu 22.04

### 🔹 Kibana Access URL

http://216.128.178.215:5601

## 📦 Kibana Installation
1. Download Kibana Package

Retrieved the Kibana .deb package download URL from the official Elastic website.

Downloaded the package using wget:
wget https://artifacts.elastic.co/downloads/kibana/kibana-8.x.x-amd64.deb

2. Install Kibana

Installed Kibana using dpkg:
dpkg -i kibana-8.x.x-amd64.deb

## Kibana Configuration

Modified the Kibana configuration file:
nano /etc/kibana/kibana.yml

## 🔹 Configuration Changes

Uncommented and modified the following settings:
server.port: 5601
server.host: "216.128.178.215"

## 🔹 Purpose
Enabled Kibana web access on port 5601
Allowed remote browser access to the Kibana interface

## ▶️ Starting Kibana Service

Reloaded system services and enabled Kibana at boot:

systemctl daemon-reexec
systemctl enable kibana
systemctl start kibana

## 🔐 Elasticsearch Enrollment Token

Generated an enrollment token to connect Kibana with Elasticsearch.

## 🔹 Navigate to Elasticsearch Binary Directory
cd /usr/share/elasticsearch/bin

## 🔹 Generate Kibana Enrollment Token
./elasticsearch-create-enrollment-token --scope kibana

The generated token was copied and saved for Kibana enrollment.

## 🌐 Accessing Kibana

Opened Kibana in a web browser:

http://216.128.178.215:5601

## ❌ Issue Encountered

Initially received the following error:

ERR_CONNECTION_TIMED_OUT

## 🛠️ Troubleshooting & Resolution

The issue was caused by restrictive Vultr firewall rules blocking inbound access to Kibana.

## 🔹 Firewall Fix

Modified the Vultr Firewall Group to allow:

Protocol: TCP
Port Range: 1-65535
Source: Personal IP Address

This allowed secure access to Kibana while still restricting unauthorized public access.

## ✅ Verification

Confirmed:

- Kibana service was running successfully
- Browser access to Kibana was operational
- Kibana could communicate with Elasticsearch using the enrollment token

📸 Screenshots

## 🔹 Vultr Firewall Configuration
![Vultr Firewall](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/screenshots/kibana-firewall-rule.png)

---

## 🔹 Ubuntu UFW Rule
![Ubuntu UFW](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/screenshots/ubuntu-ufw-rule.png)

---

## 🔹 Kibana Login Page
![Kibana Login](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/screenshots/kibana-login-page.png)

## 🔐 Security Considerations

The following security controls were implemented:

- Restricted firewall access to trusted IP addresses only
- Limited Kibana exposure to controlled inbound traffic
- Used enrollment token authentication between Elasticsearch and Kibana

## 🎯 Key Takeaways
- Successfully deployed Kibana within a cloud-hosted ELK environment
- Configured remote access for SOC monitoring activities
- Integrated Kibana with Elasticsearch using secure enrollment tokens
- Troubleshot and resolved connectivity issues caused by firewall restrictions

This deployment enabled centralized visualization, log analysis, dashboard creation, and threat monitoring capabilities for the SOC/DFIR lab.
