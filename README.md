# 🛡️ Honeypot Attack Detection & SIEM Monitoring with Cowrie + Splunk

## 📌 Overview
This project demonstrates a **real-time attack detection and monitoring pipeline** using:

- A **Cowrie SSH Honeypot**
- A simulated **attacker machine (Kali Linux)**
- A **Splunk SIEM instance** for log ingestion, analysis, dashboards, and alerts

The objective was to **simulate real attacker behavior**, capture telemetry, analyze events, and generate insights similar to a Security Operations Center (SOC) workflow.

---

## 🎯 Project Objectives

- Deploy a honeypot safely in an isolated lab  
- Simulate brute-force SSH attacks  
- Capture attacker behavior in real time  
- Stream logs to Splunk using Docker volumes  
- Build dashboards and alerts in Splunk  
- Demonstrate hands-on SOC investigation workflow  

---

## 🧰 Tools & Technologies

| Category | Technology |
|---|---|
| Honeypot | Cowrie |
| SIEM | Splunk |
| Attacker | Kali Linux |
| Container | Docker |
| OS | Ubuntu |
| Log Format | JSON |
| Analysis | SPL (Splunk) |

---

## 🖥️ Virtual Environment Setup

### Virtual Machines

| VM | OS | Purpose |
|---|---|---|
| Honeypot | Ubuntu | Cowrie + log streaming |
| Splunk | Ubuntu | SIEM analysis |
| Attacker | Kali Linux | Attack simulation |

### Networking

| VM | Adapter 1 | Adapter 2 |
|---|---|---|
| Honeypot | NAT | Host-only |
| Splunk | NAT | Host-only |
| Kali | N/A | Host-only |

### Rationale

- NAT for internet + updates  
- Host-only for a safe, isolated attack surface  

---

# 🏗️ Architecture

```mermaid
graph TD;

Attacker(Kali Linux) -->|SSH Attempts| Honeypot[Cowrie Honeypot]

Honeypot -->|JSON Logs| Volume[/opt/cowrie_logs/]

Volume --> Splunk[Splunk SIEM]

Splunk --> Dashboards
Splunk --> Alerts

Dashboards --> Analyst
Alerts --> Analyst
