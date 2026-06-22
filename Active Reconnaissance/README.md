                                            Active Reconnaissance

# Active Scanning

### T1: Host and DNS Resolution Check (host & dig)

In this task, I used both the 'host' and 'dig' commands to determine whether the target domain 'sdf.org' is live and to verify its DNS resolution status. The results confirmed that the domain is active and resolves to an IP address, indicating that the host is reachable over the internet.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/fe88f9f3-4fbe-40a1-aabc-5099e84f624e" />


### T2: DNS Enumeration and Zone Transfer Attempt (dnsenum)

In this task, I performed DNS enumeration using the 'dnsenum' tool against 'sdf.org'. The objective was to gather DNS records and test whether a zone transfer could be performed. The results showed that basic DNS records were accessible, but the zone transfer attempt was not successful, indicating that proper DNS security controls are in place.



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/48abf3eb-c529-4766-87aa-5541ff7dbc7a" />




<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/047eb029-307c-413f-8402-8a17fe7555de" />




<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/364a95d4-88e2-42e7-8239-1bd3b82933f6" />



### T3: ICMP Sweep and TCP Sweep (Nmap)

In this task, I conducted both ICMP and TCP sweeps using Nmap with the '--reason' option and disabled ARP ping to ensure accurate network-level discovery. The scan confirmed that the host responds to ICMP requests and is reachable via TCP, with Nmap providing detailed reasoning for host status and response behavior.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/f8aa85a8-9cf0-43f0-9b55-6856de2fef2a" />

##### ICMP Sweep


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/b93afa80-bbe3-4f36-980f-5238eea65364" />

##### TCP Sweep



### T4: Port Scanning and Service Detection (Nmap)

In this task, I performed a full port scan to identify open ports and the services running on 'sdf.org'. The scan revealed the active ports and associated service versions, which helps in understanding the attack surface of the target system.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/a3df41b2-7ca7-4e4e-a47f-e97bc1acb342" />



# Vulnerability Scanning

### T1: Vulnerability Detection Using NSE Scripts

In this task, I used Nmap Scripting Engine (NSE) scripts to identify known vulnerabilities on 'sdf.org'. The scan executed multiple vulnerability-related scripts and produced output highlighting potential security weaknesses, if any were detected. This step helps in assessing the security posture of the target system.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/1e479843-efcf-438c-9df4-7d0f1be10492" />


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/a9bc406e-1e95-4d4c-a1bd-77babf2dc06f" />




### T2: Brute Force Simulation Using NSE Scripts

In this task, I performed a controlled brute force test using selected NSE scripts (such as 'ftp-brute', 'http-brute', 'snmp-brute', or 'oracle-brute') against 'sdf.org'. The objective was to evaluate authentication security and resistance to password guessing attempts. The results showed whether valid credentials could be discovered or if access controls successfully prevented unauthorized login attempts.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/8cb69dff-2ae7-43d0-a977-cbd821e7e43c" />



## Lessons Learned

This lab reinforced the importance of active reconnaissance in penetration testing. I learned how tools like 'host', 'dig', 'dnsenum', and 'nmap' can be combined to gather detailed information about a target system’s network footprint. I also gained practical experience in identifying whether a system is publicly reachable and how DNS misconfigurations can expose sensitive information. Additionally, I learned that zone transfers are a critical security risk if improperly configured, as they can reveal an entire DNS structure. The Nmap scanning exercises helped me understand how ICMP and TCP responses can be interpreted to map network behavior and identify live hosts. Finally, I gained insight into how vulnerability scanning and brute force testing can reveal weaknesses in authentication systems and service configurations. Overall, this lab improved my understanding of how attackers think during reconnaissance and how defenders can reduce exposure by properly configuring network and service-level security controls.

