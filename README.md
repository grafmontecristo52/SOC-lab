<img width="1000" height="620" alt="1000014101" src="https://github.com/user-attachments/assets/149b035c-2857-40ab-82e4-ff057a935e3d" /># SOC-Lab

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

## Network

Kali (10.10.10.1), Ubuntu (10.10.10.3), and Windows (10.10.10.2) are all on the same network, 10.10.10.0/24. The Wazuh manager is isolated from Kali and the other machines — it only has access to its own IP for collecting and managing logs from the agents.
![Uploading 1000014101.svg…<svg xmlns="http://www.w3.org/2000/svg" width="1000" height="620" viewBox="0 0 1000 620" font-family="Helvetica, Arial, sans-serif">
  <!-- White background -->
  <rect width="1000" height="620" fill="#ffffff"/>

  <!-- Title -->
  <text x="500" y="45" text-anchor="middle" fill="#000000" font-size="24" font-weight="bold">SOC Lab — Схема сети</text>

  <!-- Reusable PC icon as a symbol -->
  <defs>
    <g id="pc-icon">
      <!-- monitor -->
      <rect x="-30" y="-24" width="60" height="40" rx="3" fill="#ffffff" stroke="#000000" stroke-width="2.5"/>
      <rect x="-24" y="-18" width="48" height="28" fill="#eeeeee" stroke="#000000" stroke-width="1"/>
      <!-- stand -->
      <rect x="-6" y="16" width="12" height="8" fill="#ffffff" stroke="#000000" stroke-width="2.5"/>
      <rect x="-18" y="24" width="36" height="6" rx="2" fill="#ffffff" stroke="#000000" stroke-width="2.5"/>
    </g>
    <marker id="arrowB" markerWidth="10" markerHeight="10" refX="8" refY="3" orient="auto" markerUnits="strokeWidth">
      <path d="M0,0 L0,6 L9,3 z" fill="#000000"/>
    </marker>
  </defs>

  <!-- Network line (backbone) -->
  <line x1="150" y1="330" x2="850" y2="330" stroke="#000000" stroke-width="3"/>
  <text x="500" y="320" text-anchor="middle" fill="#555555" font-size="13">Сеть 10.10.10.0/24</text>

  <!-- Kali -->
  <use href="#pc-icon" x="230" y="230"/>
  <line x1="230" y1="266" x2="230" y2="330" stroke="#000000" stroke-width="2.5" marker-end="url(#arrowB)"/>
  <text x="230" y="380" text-anchor="middle" font-size="15" font-weight="bold" fill="#000000">Kali Linux</text>
  <text x="230" y="400" text-anchor="middle" font-size="12" fill="#333333">Атакующая машина</text>
  <text x="230" y="418" text-anchor="middle" font-size="12" fill="#333333">10.10.10.1</text>

  <!-- Windows -->
  <use href="#pc-icon" x="500" y="230"/>
  <line x1="500" y1="266" x2="500" y2="330" stroke="#000000" stroke-width="2.5" marker-end="url(#arrowB)"/>
  <text x="500" y="380" text-anchor="middle" font-size="15" font-weight="bold" fill="#000000">Windows 10</text>
  <text x="500" y="400" text-anchor="middle" font-size="12" fill="#333333">Цель / агент</text>
  <text x="500" y="418" text-anchor="middle" font-size="12" fill="#333333">10.10.10.2</text>

  <!-- Ubuntu -->
  <use href="#pc-icon" x="770" y="230"/>
  <line x1="770" y1="266" x2="770" y2="330" stroke="#000000" stroke-width="2.5" marker-end="url(#arrowB)"/>
  <text x="770" y="380" text-anchor="middle" font-size="15" font-weight="bold" fill="#000000">Ubuntu</text>
  <text x="770" y="400" text-anchor="middle" font-size="12" fill="#333333">Цель / агент</text>
  <text x="770" y="418" text-anchor="middle" font-size="12" fill="#333333">10.10.10.3</text>

  <!-- Wazuh Manager, below, connected only to Windows and Ubuntu (logs) -->
  <use href="#pc-icon" x="640" y="500"/>
  <text x="640" y="550" text-anchor="middle" font-size="15" font-weight="bold" fill="#000000">Wazuh Manager</text>
  <text x="640" y="570" text-anchor="middle" font-size="12" fill="#333333">SIEM (изолирован от Kali)</text>

  <!-- Log-forwarding arrows from Windows and Ubuntu to Wazuh -->
  <line x1="500" y1="330" x2="620" y2="480" stroke="#000000" stroke-width="2.5" marker-end="url(#arrowB)"/>
  <line x1="770" y1="330" x2="660" y2="480" stroke="#000000" stroke-width="2.5" marker-end="url(#arrowB)"/>
  <text x="560" y="440" font-size="11" fill="#555555">логи</text>
  <text x="700" y="440" font-size="11" fill="#555555">логи</text>

  <!-- Legend note -->
  <text x="500" y="600" text-anchor="middle" font-size="11" fill="#777777">Kali не имеет доступа к Wazuh Manager</text>
</svg>
]()


## Tools

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


