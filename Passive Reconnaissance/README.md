                                 Passive Reconnaissance Using Shodan, WHOIS, and MITRE ATT&CK

# Overview

In this lab, I explored passive reconnaissance techniques using Shodan, WHOIS, Netcraft, and the MITRE ATT&CK framework. The objective was to identify internet-facing devices, gather publicly available information about them, analyze potential vulnerabilities, and understand how attackers and defenders interact with these weaknesses.

# Web Camera Reconnaissance

# Step 1: Identifying an Exposed Web Camera in Shodan

I logged into Shodan and searched for publicly accessible web cameras. From the search results, I selected a device that displayed both a domain name and open ports.

The information exposed by Shodan demonstrates how much device information can be publicly available when systems are connected to the internet without proper restrictions.

<img width="563" height="186" alt="image" src="https://github.com/user-attachments/assets/f77c3c51-c8b6-4c43-92d1-c4405be5aedb" />


# Step 2: Domain Investigation Using WHOIS

Using the domain name identified in Shodan, I performed a WHOIS lookup to gather additional information, including the associated IP address.

# Security Weaknesses Identified

After researching common vulnerabilities associated with IP cameras and web cameras, I found several potential security concerns:

* Unauthorized Access: Weak or default credentials can allow attackers to gain control of the device.
* Wi-Fi Security Risks: If attackers gain access to the wireless network, they may be able to access connected cameras.
* Outdated Firmware: Devices that are not regularly updated may contain known vulnerabilities that attackers can exploit.
* Unencrypted Data Transmission: Without encryption, video streams and device communications can be intercepted through man-in-the-middle attacks.
* Poor Configuration Practices: Misconfigured services can expose management interfaces directly to the internet.

These weaknesses highlight the importance of strong authentication, regular updates, network segmentation, and encrypted communications.

<img width="507" height="198" alt="image" src="https://github.com/user-attachments/assets/7d80ad29-174b-49bf-a5c0-9ef1c65a0e10" />

# Industrial Control System (ICS) Reconnaissance

# Step 1: Searching for Devices Using Port 502

Port 502 is commonly associated with Modbus, a protocol frequently used in industrial control systems (ICS). Using the Shodan search query port:502, I located a device that contained open port information and associated CVEs.

<img width="452" height="193" alt="image" src="https://github.com/user-attachments/assets/378c80eb-e3cc-42ec-a3b3-ca448cc29b96" />

<img width="452" height="201" alt="image" src="https://github.com/user-attachments/assets/89c1b397-9287-4773-99ec-61535e9b55c8" />


# Step 2: Device Analysis

Although the device identification field did not provide a specific vendor or model, the presence of Port 502 suggests that the device is likely part of an industrial control environment.

Industrial control systems often face several security challenges, including:

* Lack of authentication mechanisms in legacy protocols.
* Use of outdated firmware and software.
* Exposure of critical infrastructure to public networks.
* Vulnerability to denial-of-service attacks.
* Risk of unauthorized remote access.

Because industrial systems often prioritize availability and operational continuity, security updates may not always be applied promptly, increasing their exposure to known vulnerabilities.

# Step 3: CVE Investigation and MITRE ATT&CK Mapping

I selected CVE-2020-4487 from the Shodan vulnerability list and researched it using the MITRE CVE database.

According to MITRE, the vulnerability affects the HTTP/2 protocol and can allow denial-of-service conditions through excessive stream resets, resulting in server resource exhaustion.

# Attack Type

The vulnerability aligns with a Denial-of-Service (DoS) attack, where an attacker attempts to overwhelm system resources and disrupt normal operations.

<img width="451" height="229" alt="image" src="https://github.com/user-attachments/assets/f07a33f6-64ed-4e92-8186-1b09f1c71e89" />

<img width="451" height="226" alt="image" src="https://github.com/user-attachments/assets/bb952558-c6c7-4bf5-bf10-b9ac60af5c84" />

# Detection Method: Network Traffic Analysis

Network traffic analysis monitors communication patterns and session metadata to identify unusual behavior. Security teams can use traffic monitoring tools to detect spikes in requests, abnormal connection attempts, or patterns consistent with denial-of-service activity.

# Mitigation Method: Filter Network Traffic

Network traffic filtering helps reduce attack exposure by controlling which traffic is allowed to enter or leave the network. Security controls such as firewalls, access control lists, network segmentation, and protocol filtering can significantly reduce the likelihood of successful denial-of-service attacks.


# Lessons Learned

This lab demonstrated how much information about internet-connected devices can be collected without directly interacting with them. I learned that passive reconnaissance tools such as Shodan can reveal exposed devices, open ports, and known vulnerabilities that attackers could potentially exploit. I also gained experience using WHOIS to identify infrastructure details and understand how public records contribute to reconnaissance activities. Researching web cameras reinforced the importance of strong authentication, firmware updates, and encrypted communications. Examining industrial control systems highlighted the risks associated with legacy protocols and publicly exposed critical infrastructure. Finally, mapping a CVE to the MITRE ATT&CK framework helped me understand how vulnerabilities relate to real-world attack techniques, as well as the importance of detection and mitigation strategies in defensive security.
