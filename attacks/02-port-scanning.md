## Attack 2: Network / Port Scanning (Nmap)

- **MITRE ATT&CK:** T1046 – Network Service Discovery / T1595 – Active Scanning (Tactic: Discovery / Reconnaissance)
- **Attacker:** Kali (10.10.10.1)
- **Target:** Ubuntu (10.10.10.3)
- **Tools used:** Nmap,Suricata

### Attack Steps
1. Run a discovery scan: `nmap -Pn -n -sS -p 1-1000 10.10.10.3`
2. Note the number of ports scanned and the timing profile

### Detection
- Detected via Wazuh log analysis of connection attempts (many ports, single source IP, short time window) paired with Suricata/IDS.
- Rule logic: flag a source IP hitting N distinct destination ports within a short time window as a port scan.

### Timeline
- Attack start: 21:50:45
- First scan-related log: 21:50:45
- Alert fired: 21:53
- Detection delay: 2 min 15 sec.

### Screenshots
1. Nmap scan output
<img width="586" height="346" alt="nmap scan" src="https://github.com/user-attachments/assets/ddbf15c1-2f10-42d4-8023-75bbae287516" />
2.Wazuh/IDS alert dashboard showing scan detection
<img width="1697" height="43" alt="nmap dash" src="https://github.com/user-attachments/assets/7dc61586-a593-4e43-a7dc-7a5b84b5c61c" />
### Response / Remediation
- Block/rate-limit the offending IP.
- Review exposed services and close unnecessary ports.
- Flag as reconnaissance — treat as an early warning of a larger intrusion attempt.



---
