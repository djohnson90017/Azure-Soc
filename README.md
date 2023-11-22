# Honeynet In Azure 
![Cloud Honeynet / SOC])



![Honeypot  (1)](https://github.com/djohnson90017/Azure-Soc/assets/149316775/1f746b3e-a07d-4f39-a963-97540a19405f)

## Introduction

In this project, I embarked on the endeavor of constructing a mini honeynet within the confines of the Azure cloud environment. Subsequently, I meticulously gathered log data from a diverse range of sources and meticulously channeled it into a Log Analytics workspace. This centralized repository served as the cornerstone for Microsoft Sentinel, empowering it to meticulously construct attack maps, proactively trigger alerts, and effectively generate incidents. With meticulous precision, I delved into the heart of the insecure environment, meticulously measuring security metrics over a 24-hour period. Following this, I diligently implemented a series of stringent security controls to fortify the environment, subjecting it to another 24-hour metrics measurement cycle. The results of this rigorous testing are presented below, encompassing the following security metrics:

SecurityEvent: Windows Event Logs
Syslog: Linux Event Logs
SecurityAlert: Log Analytics Alerts Triggered
SecurityIncident: Incidents created by Sentinel
AzureNetworkAnalytics_CL: Malicious Flows allowed into our honeynet

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

Mini Honeynet Architecture in Azure

The mini honeynet in Azure comprises the following components:

Virtual Network (VNet): Provides a secure isolation layer for the honeynet environment.

Network Security Group (NSG): Enforces granular traffic control rules to restrict unauthorized access to the honeynet.

Virtual Machines (VMs): Serve as honeypot systems that mimic vulnerable targets to attract and deceive attackers.

Log Analytics Workspace: Collects and centralizes logs from honeynet components for comprehensive monitoring and analysis.

Azure Key Vault: Safeguards sensitive credentials and secrets used by the honeynet infrastructure.

Azure Storage Account: Stores log data and other honeynet artifacts for future reference and investigation.

Microsoft Sentinel: Provides security intelligence and threat detection capabilities to identify and respond to potential threats.

BEFORE Metrics

Initially, all resources were exposed to the internet, allowing unrestricted access from malicious actors. The Virtual Machines had both their Network Security Groups and built-in firewalls disabled, and all other resources lacked private endpoints, making them vulnerable to public attacks.

AFTER Metrics

To enhance security, Network Security Groups were hardened by blocking all incoming traffic except for authorized connections from the administrator's workstation. Additionally, all resources were protected by their built-in firewalls and private endpoints, effectively shielding them from unauthorized access.

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/1qvswSX.png)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/G1YgZt6.png)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/ESr9Dlv.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-03-15 17:04:29
Stop Time 2023-03-16 17:04:29

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 19470
| Syslog                   | 3028
| SecurityAlert            | 10
| SecurityIncident         | 348
| AzureNetworkAnalytics_CL | 843

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-03-18 15:37
Stop Time	2023-03-19 15:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8778
| Syslog                   | 25
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
