## Attack 2: Network / Port Scanning (Nmap)

- **MITRE ATT&CK:** T1046 – Network Service Discovery / T1595 – Active Scanning (Tactic: Discovery / Reconnaissance)
- **Attacker:** Kali (10.10.10.1)
- **Target:** Entire subnet 10.10.10.0/24
- **Tools used:** Nmap

### Attack Steps
1. Run a discovery scan across the subnet: `nmap -sn 10.10.10.0/24`
2. Run an aggressive scan against identified hosts: `nmap -A 10.10.10.2 10.10.10.3`
3. Note the number of ports scanned and the timing profile (`-T4`/`-T5` vs default).

### Detection
- Detected via Wazuh log analysis of connection attempts (many ports, single source IP, short time window), optionally paired with Suricata/IDS signatures if added.
- Rule logic: flag a source IP hitting N distinct destination ports within a short time window as a port scan.

### Timeline
- Attack start: [fill in]
- First scan-related log: [fill in]
- Alert fired: [fill in]
- Detection delay: [fill in] seconds

### Screenshots
1. Nmap scan output
2. Wazuh/IDS alert dashboard showing scan detection
3. Raw log showing multiple port connection attempts from one IP

### Response / Remediation
- Block/rate-limit the offending IP.
- Review exposed services and close unnecessary ports.
- Flag as reconnaissance — treat as an early warning of a larger intrusion attempt.



---
