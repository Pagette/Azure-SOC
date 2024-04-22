# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction

In this project, I built a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

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
<img width="771" alt="image" src="https://github.com/Pagette/Azure-SOC/assets/167459764/82a3a9d5-3801-4c20-b855-2e715cdf86c6">
<img width="734" alt="image" src="https://github.com/Pagette/Azure-SOC/assets/167459764/a6883e68-c4dc-4db7-bc32-d82d7434c967">
<img width="657" alt="image" src="https://github.com/Pagette/Azure-SOC/assets/167459764/a3ae3d86-4303-4862-882b-09bb5eff895a">
<img width="600" alt="image" src="https://github.com/Pagette/Azure-SOC/assets/167459764/1a304239-90fb-4a8b-be72-2e5253d8e925">

## Metrics Before Hardening / Security Controls

The following table shows the metrics I measured in the insecure environment for 24 hours:
Start Time	4/3/2024, 8:15:21 PM
Stop Time	4/4/2024, 8:15:21 PM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 10285
| Syslog                   | 3086
| SecurityAlert            | 4
| SecurityIncident         | 161
| AzureNetworkAnalytics_CL | 2481

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time	4/10/2024, 9:47:25 PM
Stop Time	4/11/2024, 9:47:25 PM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8432
| Syslog                   | 1
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a small honeynet was established within Microsoft Azure, with log sources seamlessly integrated into a Log Analytics workspace. I employed Microsoft Sentinel to trigger alerts and create incidents based on the ingested logs. Moreover, we conducted metric evaluations within the vulnerable environment both before and after implementing the security protocols. Remarkably, the implementation of these security measures led to a significant reduction in both security events and incidents, underscoring their efficacy.

It's important to acknowledge that had the network resources been extensively utilized by regular users, there might have been a higher frequency of security events and alerts during the 24-hour period post-security implementation.
