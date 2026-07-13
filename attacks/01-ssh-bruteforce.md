



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
- Attack start: 21:49
- First failed login logged: 21:49:46
- Alert fired: 21:49:50
- Detection delay: 4 seconds

### Screenshots
1. Hydra running against the target
<img width="749" height="206" alt="hydra ssh" src="https://github.com/user-attachments/assets/5590cdad-7bad-4bbe-a8ad-52cde938e5e8" />
2. Wazuh dashboard showing the triggered brute-force alert
<img width="910" height="124" alt="alert" src="https://github.com/user-attachments/assets/796ffa4e-6f05-4592-a042-638cd2869a29" />
3. Raw log/JSON of the authentication failure event
<img width="1920" height="860" alt="more log ssh" src="https://github.com/user-attachments/assets/ce359674-f593-45be-89fe-7b1eba8ec4f8" />

### Response / Remediation
- Block source IP via firewall/iptables.
- Enforce account lockout policy or fail2ban.
- Recommend key-based SSH auth instead of passwords.

### Takeaway


---

