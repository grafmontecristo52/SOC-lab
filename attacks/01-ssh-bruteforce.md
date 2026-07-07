


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

