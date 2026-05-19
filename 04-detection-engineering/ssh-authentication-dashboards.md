# SSH Authentication Dashboards & Geolocation Visualization

## 📌 Objective
To create dashboards and geolocation visualizations for SSH authentication activity within the SOC environment.

The dashboards provide:
- Failed SSH authentication visibility
- Successful SSH authentication monitoring
- Geographic attack source visualization
- Centralized authentication monitoring

---

# 🌍 Failed SSH Authentication Dashboard

## 🔹 Query Development

Created a KQL query to identify failed SSH authentication events.

---

## 🔹 KQL Query

kql
system.auth.ssh.event : * and agent.name: "MYDFIR-Linux-Tee" and system.auth.ssh.event: "Failed"

---

## 🗺️ Geolocation Visualization

Navigated to:

Kibana → Maps

# 🔹 Visualization Configuration

Configured:

- Source layer using authentication logs
- Geolocation mapping based on source.ip
- Choropleth visualization

# 🔹 EMS Boundaries

Selected:

EMS Boundaries → World Countries

This enabled geographic visualization of attack origins.

---

## 💾 Dashboard Save

Saved the visualization as:

SSH Failed Authentications - Network Map

Added the visualization to a new dashboard.

---

## ✅ Failed Authentication Visibility

The dashboard successfully displayed:

- Failed SSH authentication activity
- Source IP geolocation
- Attacking countries
- Authentication patterns

---

## 🔓 Successful SSH Authentication Dashboard

Duplicated the failed authentication dashboard and modified the KQL query.

# 🔹 Successful Authentication Query
system.auth.ssh.event : * and agent.name: "MYDFIR-Linux-Tee" and system.auth.ssh.event: "Accepted"

---

## 💾 Dashboard Save

Saved the updated visualization for successful SSH login monitoring.

This dashboard enabled:

- Monitoring legitimate SSH logins
- Geographic visibility of successful access
- Remote authentication tracking

---

## 📊 Final Dashboard Environment

At completion:

- SSH brute-force alert operational
- Failed authentication dashboard created
- Successful authentication dashboard created
- Geographic attack source visualization enabled

---

## 🔹 Failed SSH Dashboard
![Failed SSH Dashboard](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/failed-ssh-dashboard.png)

---

## 🔹 Successful SSH Dashboard
![Successful SSH Dashboard](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/successful-ssh-dashboard.png)

---

## 🔹 Final Dashboard Overview
![Final Dashboard Overview](https://raw.githubusercontent.com/omotara100/MyDFIR-SOC-Project/main/screenshots/final-ssh-dashboard-overview.png)

---

## 🔐 Security Value

These dashboards improve:

SSH authentication visibility
Attack source attribution
Brute-force monitoring
Geographic threat awareness
SOC investigation efficiency

---

## 🎯 Key Takeaways
- Created SSH brute-force detection alerts
- Developed authentication monitoring dashboards
- Visualized attack origins using Elastic Maps
- Implemented KQL-based detection engineering
- Improved Linux authentication monitoring capabilities

This phase established active threat monitoring and visualization capabilities within the SOC/DFIR environment.
