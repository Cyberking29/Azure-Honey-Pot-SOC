# Azure HoneyPot : Simulating Real-World Cyber Attacks
![Cloud Honeynet / SOC](https://imgur.com/jyGKCvp.png)

## Introduction

 I used Microsoft Azure to set up a honeynet and collect logs from various sources. I then used the Microsoft Sentinel tool to create incident triggers, attack maps, and alerts. I monitored the metrics collected in the insecure environment for 24 hours, and then I applied security measures to harden the system.
After collecting the metrics, I used them to visualize the locations of the attackers and summarize the system's overall improvement. I also conducted a variety of attacks against it.


## Objective
The goal of the project was to set up vulnerable virtual machines in Azure. This would allow me to analyze and study cyber attacks. Doing so would allow me to gain a deeper understanding of how attackers operate. It also showcased my ability to quickly respond to certain issues.

## Technologies, Regulations, and Azure Components Employed:

- Azure Virtual Network (VNet)
- Azure Network Security Group (NSG)
- Virtual Machines (2x Windows, 1x Linux)
- Log Analytics Workspace with Kusto Query Language (KQL) Queries
- Azure Key Vault for Secure Secrets Management
- Azure Storage Account for Data Storage
- Microsoft Sentinel for Security Information and Event Management (SIEM)
- Microsoft Defender for Cloud to Protect Cloud Resources
- Windows Remote Desktop for Remote Access
- Command Line Interface (CLI) for System Management
- PowerShell for Automation and Configuration Management
- [NIST SP 800-53 Revision 5](https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final) for Security Controls
- [NIST SP 800-61 Revision 2](https://www.nist.gov/privacy-framework/nist-sp-800-61) for Incident Handling Guidance

## Methodology

- <b>*Creating the honeynet*</b>: I began by [deploying multiple vulnerable virtual machines]in Azure, simulating an insecure environment.

- <b>*Monitoring and analysis*</b>: Azure was configured to ingest log sources from various resources into a log analytics workspace. Microsoft Sentinel was then used to build attack maps, trigger alerts, and create incidents based on the collected data.

- <b>*Security metrics measurement*</b>: I observed the environment for 24 hours, recording key security metrics while it was insecure. This provided a baseline to compare against after implementing remediation measures.

- <b>*Incident response and remediation*</b>: After addressing the incidents and identifying vulnerabilities, I began the process of hardening the environment by applying security best practices and Azure-specific recommendations.

- <b>*Post-remediation analysis*</b>: I re-observed the environment for another 24 hours to measure security metrics again, comparing the results with the initial baseline.


## Architecture Prior to Implementing Hardening Measures and Security Controls
![Architecture Diagram](https://i.imgur.com/1tLjWY9.png)

<b>Before Hardening Measures and Security Controls:</b>

- All resources were initially exposed to the internet in the "BEFORE" phase. This security setup was designed to attract potential attackers and observe their activities. The virtual machines had built-in firewalls that allowed unrestricted access.
Other resources, such as databases and storage accounts, were also exposed to the internet without using Private Endpoints.


## Architecture After Implementing Hardening Measures and Security Controls
![Architecture Diagram](https://imgur.com/6nPku03.png)
 <b>As part of the AFTER phase, I implemented various security controls and hardening measures to improve the overall security posture of the environment. included:</b>

- <b>Network Security Groups (NSGs)</b>: I hardened the NSGs by blocking all inbound and outbound traffic, with the sole exception of my own public IP address. This ensured that only authorized traffic from a trusted source was allowed to access the virtual machines.

- <b>Built-in Firewalls</b>: I configured the built-in firewalls on the virtual machines to restrict access and protect the resources from unauthorized connections. This step involved fine-tuning the firewall rules based on the specific requirements of each VM, thereby minimizing the potential attack surface.

- <b>Private Endpoints</b>: To enhance the security of other Azure resources, I replaced the public endpoints with Private Endpoints. This ensured that access to sensitive resources, such as storage accounts and databases, was limited to the virtual network and not exposed to the public internet. As a result, these resources were protected from unauthorized access and potential attacks.

By comparing the security metrics before and after implementing these hardening measures and security controls, I was able to demonstrate the effectiveness of each step in improving the overall security posture of the Azure environment.

## Attack Maps Before Hardening / Security Controls
<br />
 <br />
 <br />
 
- <b>This attack map demonstrates the consequences of leaving the Network Security Group (NSG) open, as it allowed for malicious traffic to flow unimpeded. This visualization underscores the importance of implementing proper security measures, such as restricting NSG rules, to prevent unauthorized access and minimize potential threats.</b>


![NSG Allowed Inbound Malicious Flows](https://imgur.com/ltC5QwE.png)<br>

 <br />
 <br />
 
 - <b>This attack map highlights the numerous syslog authentication failures experienced by the Linux server I deployed, indicating that unauthorized access attempts were made from outisde. This serves as a reminder of the importance of securing Linux servers with strong authentication mechanisms and monitoring system logs for signs of intrusion attempts.</b>
 
![Linux Syslog Auth Failures](https://imgur.com/HLLT0H4.png)<br>

 <br />
 <br />
 
 - <b>This attack map showcases numerous RDP and SMB failures, illustrating the persistent attempts by potential attackers to exploit these protocols. The visualization emphasizes the need for securing remote access and file sharing services to protect against unauthorized access and potential cyber threats.</b>
 
![Windows RDP/SMB Auth Failures](https://imgur.com/yr7CyoR.png)<br>

 <br />
 <br />

## Attack Maps After Hardening / Security Controls

> All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.

 <br />
 <br />
 
## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-06-20 01:28:00 AM
Stop Time 2023-06-21 01:28:00 AM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent (Windows VM)            | 131255
| Syslog (Linux VM)                   | 6734
| SecurityAlert (Microsoft Defender for Cloud            | 3
| SecurityIncident (Sentinel Incidents)        | 51
| NSG Inbound Malicious Flows Allowed | 2883



## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-06-24 04:11 PM
Stop Time	2023-06-25 04:11 PM


| Metric                   | Count
| ------------------------ | -----
| SecurityEvent (Windows VM)            | 10954
| Syslog (Linux VM)                   | 25
| SecurityAlert (Microsoft Defender for Cloud            | 0
| SecurityIncident (Sentinel Incidents)        | 0
| NSG Inbound Malicious Flows Allowed | 0

## Conclusion
I used Microsoft Azure's cloud infrastructure to establish a honeynet. The platform's security features, such as Microsoft Sentinel, generated alarms and triggered incidents based on the collected logs. Before implementing any security controls, baseline metrics were monitored in the cloud.
A variety of security measures were then implemented to fortify the network. After the controls were added, further measurements were taken.


Comparing pre- and post-implementation metrics demonstrated a significant reduction in security events and incidents, highlighting the effectiveness of the enforced security controls.
If regular users extensively engaged the network's resources, it's plausible that a higher number of security events and alerts could have been produced within the 24-hour timeframe post-security control implementation.
