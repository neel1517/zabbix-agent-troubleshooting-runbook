# zabbix-agent-troubleshooting-runbook
# Zabbix Agent Troubleshooting & Monitoring Automation Runbook

![Zabbix](https://img.shields.io/badge/Zabbix-Monitoring-red)
![Linux](https://img.shields.io/badge/Linux-Administration-blue)
![DevOps](https://img.shields.io/badge/DevOps-Infrastructure-green)
![Bash](https://img.shields.io/badge/Scripting-Bash-black)

---

## Overview

This repository documents real-world **Zabbix monitoring setup, troubleshooting, and production issue resolution** across multiple Linux servers.

It includes practical fixes for:
- Zabbix agent installation and configuration
- Sudo permission issues for custom scripts
- Systemd service failures
- Network and firewall issues (port 10050)
- Host interface and connectivity problems
- Production monitoring stability improvements

---

## 🏗️ Architecture
                 Zabbix Server
              (Frontend + DB)
                      |
                   TCP 10050
                      |
        ---------------------------------
        |               |               |
     Server 1       Server 2        Server 3
      Agent          Agent           Agent

  
---

## Features

- Centralized infrastructure monitoring using Zabbix Agent
- Secure execution of custom monitoring scripts via sudoers configuration
- Automated troubleshooting and validation scripts
- Standardized agent configuration across multiple servers
- Production-ready runbook for incident handling

---

## Issues Identified & Resolved

### Sudo Permission Issue
- Error: `sudo: no tty present and no askpass program specified`
- Fix: Configured passwordless sudo using `/etc/sudoers.d/zabbix`
- Impact: Enabled automated execution of monitoring scripts

---

### Host Interface Issue
- Error: `Cannot find host interface for item key "agent.hostname"`
- Fix: Added proper Zabbix agent interface (IP/DNS + port 10050)
- Impact: Enabled successful template/item assignment

---

### Log File Issue
- Error: `cannot open log file /var/log/zabbix/zabbix_agentd.log`
- Fix: Created log directory and set correct ownership
- Impact: Restored agent startup functionality

---

### Permission Issue
- Error: `Operation not permitted`
- Fix: Used sudo for secure system configuration changes
- Impact: Ensured controlled administrative access

---

### Agent Connectivity Issue
- Error: Empty response from agent
- Fix: Corrected `Server=` configuration in agent config
- Impact: Restored stable communication with Zabbix server

---

### Network Timeout Issue
- Error: `TCP connection timed out on port 10050`
- Fix: Opened firewall / AWS Security Group for port 10050
- Impact: Enabled remote monitoring connectivity

---

##  Example Scripts

###  Fix Sudo Permissions
```bash
#!/bin/bash

echo "Configuring Zabbix sudo access..."

echo "zabbix ALL=(ALL) NOPASSWD: /etc/zabbix/zabbix_agentd.d/getdata.sh" \
| sudo tee /etc/sudoers.d/zabbix

sudo chmod 440 /etc/sudoers.d/zabbix

echo "Done"

## Monitoring Flow:
Zabbix Server
     ↓
TCP Request (10050)
     ↓
Zabbix Agent (Linux Host)
     ↓
Custom Scripts / System Metrics
     ↓
Zabbix Server Database
     ↓
Dashboard Visualization

###  Key Learnings

- Zabbix agent architecture and monitoring workflow  
- Linux system administration in production environments  
- Firewall and network troubleshooting (AWS + Linux)  
- Sudoers configuration and security management  
- Systemd service debugging and recovery  
- Production-grade monitoring reliability improvements  

---
###  Outcome

- Stabilized Zabbix monitoring across multiple servers  
- Resolved multiple production-level agent failures  
- Improved infrastructure observability  
- Standardized monitoring setup and troubleshooting approach  

---

### Author

**Senior DevOps / Linux Engineer**  
Focus: Monitoring | Automation | Infrastructure | Zabbix | Linux Systems
