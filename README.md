 # SOC-lab


For best practise and learning i decide to use 4 machine.
- **Wazuh v4.14.5 OVA**(SIEM manager wich connected with Windows and Ubuntu agents to collect and filtered logs)
- **Windows 10 machine**
- **Ubuntu machine**
- **Kali**(Cracker)

## Network
Kali(10.10.10.1) , Ubuntu(10.10.10.3) and Windows(10.10.10.2) machines has the same network 10.10.10.0/24
Wazuh was issolated from kali and others machine , he only has acces too his ip for collecting logs and manage them for me.
## Tools
- Nmap , Hydra 
- Metasploit Framework
- Claude , DeepSeek for srcipts


## Why Wazuh instead other SIEM (e.g Splunk, ELK, MAXPATROL..)
The Wazuh is full free and open source cybersecurity tool thah intigrate themshelve (EDR,CLOUD DEFENSE,FIM,INTEGRATION WITH GITHUB,MITTRE ATTACK AND OTHERS PRETTY INTERISTING AND GOOD STUF FOR SOC TEAM AND PROJECT)
He's very friendly for the new people in the cybersecurity! Has own very good and useful documentation . Very simple to download and manage OVA version 
