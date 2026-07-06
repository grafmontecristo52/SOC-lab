 # SOC-lab


For best practise and learning i decided to use 4 machines.
- **Wazuh v4.14.5 OVA**(SIEM manager wich connected with Windows and Ubuntu agents to collect and forward logs)
- **Windows 10 machine**
- **Ubuntu machine**
- **Kali**(Cracker)

## Network
Kali(10.10.10.1) , Ubuntu(10.10.10.3) and Windows(10.10.10.2) machines has the same network 10.10.10.0/24
Wazuh was isolated from kali and others machine , he only has access only to its own ip for collecting logs and manage them for me.
## Tools
- Nmap , Hydra 
- Metasploit Framework
- Claude , DeepSeek for srcipts


## Why Wazuh instead other SIEM (e.g Splunk, ELK, MAXPATROL..)
The Wazuh is full free and open source cybersecurity tool thah integrates (EDR,CLOUD DEFENSE,FIM,INTEGRATION WITH GITHUB,MITTRE ATTACK AND OTHERS PRETTY INTERISTING AND GOOD STUFF FOR SOC TEAM AND PROJECT)
It's very friendly for the new people in the cybersecurity! Has own very good and useful documentation . Very simple to download and manage OVA version 
