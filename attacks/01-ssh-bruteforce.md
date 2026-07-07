# Attack Scenarios — SOC-Lab


---

## Attack 1: SSH Brute Force (Hydra)

- **MITRE ATT&CK:** T1110 – Brute Force (Tactic: Credential Access)
- **Attacker:** Kali (10.10.10.1)
- **Target:** Ubuntu (10.10.10.3), SSH service
- **Tools used:** Hydra , nmap

### Attack Steps
1. Identify SSH service open on Ubuntu target (port 22) with "sudo nmap -Pn -n -p 22 10.10.10.3"
2. Use Hydra with a wordlist against the SSH service:
   `hydra -l user -P 10k-most-common.txt -t 6 ssh://10.10.10.3`
3. Observe successful/failed login attempts on the target on the dashboard wazuh.

### Detection
- Wazuh rule group: `authentication_failures`
- Custom rule: trigger on 5+ failed SSH logins from the same source IP within 60 seconds → alert level 10.
- Rule logic: aggregate failed `sshd` auth events by `srcip`, threshold-based correlation.

### Timeline
- Attack start: 21:49:46
- First failed login logged: [fill in]
- Alert fired: [fill in]
- Detection delay: [fill in] seconds

### Screenshots
1. Hydra running against the target
2. Wazuh dashboard showing the triggered brute-force alert
3. Raw log/JSON of the authentication failure event

### Response / Remediation
- Block source IP via firewall/iptables.
- Enforce account lockout policy or fail2ban.
- Recommend key-based SSH auth instead of passwords.

### Takeaway
Demonstrates understanding of credential access techniques, ability to configure/tune correlation-based detection rules (not just use defaults), and knowledge of practical remediation steps.

---

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

### Takeaway
Demonstrates knowledge of the reconnaissance phase of the Cyber Kill Chain and the importance of catching an attack at its earliest stage, before exploitation occurs.

---

## Attack 3: Exploitation via Metasploit

- **MITRE ATT&CK:** T1210 – Exploitation of Remote Services (Tactic: Lateral Movement), plus T1059 – Command and Scripting Interpreter and/or T1068 – Exploitation for Privilege Escalation
- **Attacker:** Kali (10.10.10.1)
- **Target:** Windows (10.10.10.2) or Ubuntu (10.10.10.3), unpatched/vulnerable service
- **Tools used:** Metasploit Framework

### Attack Steps
1. Identify a vulnerable/unpatched service on the target (e.g. via prior Nmap scan).
2. Select and configure the matching Metasploit exploit module.
3. Launch the exploit to obtain a shell on the target.
4. Execute a post-exploitation action (e.g. create a new user, run a command) to simulate impact.

### Detection
- Wazuh File Integrity Monitoring (FIM) for unexpected file/system changes.
- Sysmon (Windows) + Wazuh integration for process creation monitoring.
- Alert on suspicious process execution or new user/account creation.

### Timeline
- Attack start: [fill in]
- Exploit executed: [fill in]
- Alert fired: [fill in]
- Detection delay: [fill in] seconds

### Screenshots
1. Metasploit exploit execution and shell obtained
2. Wazuh alert dashboard (FIM/process alert)
3. Raw log/JSON showing the indicator that triggered the alert

### Response / Remediation
- Isolate the compromised host from the network.
- Identify and patch the exploited vulnerability.
- Review for persistence mechanisms and remove any unauthorized accounts.
- Escalate to full incident response if lateral movement is suspected.

### Takeaway
This is the strongest demo for an interview — it shows the full attack lifecycle: exploitation → post-exploitation impact → detection → containment/response, tying together detection engineering and incident response skills in one scenario.
