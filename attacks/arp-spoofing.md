
## Attack 3: ARP spoofing

- **MITRE ATT&CK:** T1210 – Exploitation of Remote Services (Tactic: Lateral Movement), plus T1059 – Command and Scripting Interpreter and/or T1068 – Exploitation for Privilege Escalation
- **Attacker:** Kali (10.10.10.1)
- **Target:** Ubuntu (10.10.10.3)
- **Tools used:** arpspoof , wireshark

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
- Attack start: 
- Exploit executed: 
- Alert fired: 
- Detection delay: 

### Screenshots
1. Metasploit exploit execution and shell obtained
2. Wazuh alert dashboard (FIM/process alert)
3. Raw log/JSON showing the indicator that triggered the alert

### Response / Remediation
- Isolate the compromised host from the network.
- Identify and patch the exploited vulnerability.
- Review for persistence mechanisms and remove any unauthorized accounts.
- Escalate to full incident response if lateral movement is suspected.
