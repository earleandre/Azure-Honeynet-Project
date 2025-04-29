# Building a SOC + Honeynet in Azure (Live Traffic)
![image](https://github.com/user-attachments/assets/3598c95e-64de-45d7-8e92-3f65203c1871)



## Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![image](https://github.com/user-attachments/assets/a332aba3-ea98-41a6-aa83-7f8fed787cf6)

## Architecture After Hardening / Security Controls
![image](https://github.com/user-attachments/assets/f34d54fd-1444-4f20-bc9e-734c348fba3b)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
![image](https://github.com/user-attachments/assets/c51b1925-5953-4a6e-9f57-0092d54d5e90)
![image](https://github.com/user-attachments/assets/48b2ab2c-b110-4402-b353-95a4f7ca78a7)
![image](https://github.com/user-attachments/assets/ae154bb4-558b-4c2b-a423-b1d4a049c649)


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2025-04-07 09:54:17
Stop Time 2025-04-08 09:54:17

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 1308
| Syslog                   | 8518
| SecurityAlert            | 06
| SecurityIncident         | 212
| AzureNetworkAnalytics_CL | 103

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-03-18 15:37
Stop Time	2023-03-19 15:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 450
| Syslog                   | 0
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
