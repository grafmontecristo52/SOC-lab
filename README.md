
## Goal

This project is a home-built SOC (Security Operations Center) lab designed to practice log collection, threat detection, alert triage, and incident response using a real SIEM (Wazuh). The goal is to simulate common attack techniques, detect them, and document the full analyst workflow — from raw attack to alert to response
## Lab Overview

For best practice and learning, I decided to use 4 machines:

| Machine | Role | OS | IP |
|---|---|---|---|
| Wazuh Manager | SIEM manager, connected with Windows and Ubuntu agents to collect and forward logs | Wazuh v4.14.5 (OVA) | .... |
| Windows 10 | Monitored endpoint / attack target | Windows 10 | 10.10.10.2 |
| Ubuntu | Monitored endpoint / attack target | Ubuntu | 10.10.10.3 |
| Kali | Attacker machine | Kali Linux | 10.10.10.1 |
| Metasploit 2 |  Monitored endpoint / attack target | Linux | 10.10.10.4 |

## Network

Kali (10.10.10.1), Ubuntu (10.10.10.3), and Windows (10.10.10.2) are all on the same network, 10.10.10.0/24. The Wazuh manager is isolated from Kali and the other machines — it only has access to its own IP for collecting and managing logs from the agents.
<img width="1300" height="950" alt="1000014139" src="https://github.com/user-attachments/assets/5a0d1c12-7e95-4308-9bab-e93d8cc44df2" />

## Tools
- Wazuh
- Suricata
- Metasploit 2

**Attack tools:**
- Nmap
- Hydra
- Metasploit Framework

**Assistance / scripting tools:**
- Claude, DeepSeek (used for scripting help and research)

## Why Wazuh instead of other SIEMs (e.g. Splunk, ELK, MaxPatrol)

Wazuh is a fully free and open-source cybersecurity tool that integrates several capabilities in one place (EDR, cloud defense, FIM, GitHub integration, MITRE ATT&CK mapping, and more). It's very friendly for people new to cybersecurity, has good and useful documentation, and is simple to download and manage as an OVA.

## Attack Scenarios

Full write-ups with detection logic, screenshots, and analyst response for each simulated attack:

- [Attack 1: SSH Brute Force](./attacks/01-ssh-bruteforce.md)
- [Attack 2: Network/Port Scanning](./attacks/02-port-scanning.md)
- [Attack 3: Exploitation via Metasploit](./attacks/03-exploitation-metasploit.md)

## Screenshots



## Lessons Learned / Next Steps


