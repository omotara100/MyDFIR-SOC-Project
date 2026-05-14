# 01-Lab-Setup README

## 📌 Overview

This section documents the deployment and initial configuration of the SOC/DFIR lab infrastructure used throughout the project.

The goal of the lab setup phase was to:

* Build a cloud-hosted SIEM environment
* Configure secure networking
* Prepare infrastructure for centralized log ingestion
* Simulate a realistic enterprise SOC architecture

---

# 🏗️ Lab Infrastructure

| Component               | Purpose                                         |
| ----------------------- | ----------------------------------------------- |
| Vultr Cloud Environment | Hosts all infrastructure                        |
| VPC Network             | Provides internal communication between servers |
| Elasticsearch Server    | Centralized log storage and indexing            |
| Kibana                  | Visualization and analysis platform             |
| Fleet Server            | Centralized Elastic Agent management            |
| Windows Endpoint        | Generates Windows telemetry                     |
| Ubuntu Endpoint         | Generates Linux telemetry                       |
| Kali Linux              | Attack simulation platform                      |
| Mythic C2               | Command-and-control simulation                  |
| Ticketing System        | Incident tracking and workflow management       |

---

# ☁️ Vultr VPC Deployment

## 📌 Objective

To create a secure private network environment for internal SOC infrastructure communication.

## 🔹 Steps Performed

1. Created a VPC network in Vultr
2. Configured private subnet: `172.31.0.0/24`
3. Attached infrastructure servers to the VPC
4. Verified internal network communication

---

# 📦 Elasticsearch Deployment

## 📌 Objective

To deploy and configure Elasticsearch as the backend SIEM data store.

## 🔹 Deployment Summary

* Ubuntu 22.04 server deployed in Vultr
* Elasticsearch package installed using `.deb` package
* Configured network access and HTTP port
* Restricted access using Vultr Firewall Groups
* Verified service functionality

---

# 🔐 Security Considerations

During deployment, the following security measures were implemented:

* Private networking using Vultr VPC
* Firewall restrictions limiting access to trusted IP addresses
* Controlled exposure of Elasticsearch HTTP interface
* Segmentation of attacker infrastructure from analyst systems

---

# 🧠 Skills Demonstrated

* Cloud infrastructure deployment
* Secure network architecture design
* Linux server administration
* SIEM deployment and configuration
* Firewall and access control management
* Infrastructure documentation

---

# 🔗 Related Project Sections

| Section                  | Link                                                                                    |
| ------------------------ | --------------------------------------------------------------------------------------- |
| Main Repository          | [MyDFIR-SOC-Project](https://github.com/omotara100/MyDFIR-SOC-Project)                  |
| Lab Setup Directory      | [01-lab-setup](https://github.com/omotara100/MyDFIR-SOC-Project/tree/main/01-lab-setup) |

# 🚀 Outcome

The lab setup phase successfully established the foundational infrastructure required for:

* Centralized log collection
* Threat detection engineering
* Attack simulation
* Threat hunting
* Incident response workflows

This environment serves as the operational backbone for all future SOC and DFIR activities documented throughout the project.

---

# 📂 Repository Reference

| Project                               | Repository                                                             | Lab Setup                                                                               |
| ------------------------------------- | ---------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| ELK Stack Deployment & Administration | [MyDFIR-SOC-Project](https://github.com/omotara100/MyDFIR-SOC-Project) | [01-lab-setup](https://github.com/omotara100/MyDFIR-SOC-Project/tree/main/01-lab-setup) |
