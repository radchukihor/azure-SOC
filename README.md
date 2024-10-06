# azure-SOC

🔥 Building a SOC + Honeynet in Azure (Live Traffic) 🚀

![68747470733a2f2f692e696d6775722e636f6d2f5a5778653033652e6a7067](https://github.com/user-attachments/assets/ee9189a8-433f-4cf3-a6de-456539095bb6)

Introduction

In this project, I built a mini honeynet in Azure, ingesting log sources from various resources into a Log Analytics workspace. This data is then processed by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents.

I measured security metrics in an insecure environment for 24 hours, applied security controls to harden the environment, and then measured metrics for another 24 hours to observe the impact of the hardening process.

📊 Metrics Monitored:

	•	SecurityEvent (Windows Event Logs)
	•	Syslog (Linux Event Logs)
	•	SecurityAlert (Log Analytics Alerts Triggered)
	•	SecurityIncident (Incidents created by Sentinel)
	•	AzureNetworkAnalytics_CL (Malicious Flows allowed into the honeynet)

🏗️ Architecture

Before Hardening / Security Controls 🔓

![68747470733a2f2f692e696d6775722e636f6d2f614244776e4b622e6a7067](https://github.com/user-attachments/assets/0057f52c-cc7e-4e03-b399-f7b77211e653)

	•	Virtual Network (VNet)
	•	Network Security Group (NSG)
	•	Virtual Machines (2 Windows, 1 Linux)
	•	Log Analytics Workspace
	•	Azure Key Vault
	•	Azure Storage Account
	•	Microsoft Sentinel

All resources were exposed to the Internet with public endpoints. Both the Network Security Groups and built-in firewalls were fully open.

After Hardening / Security Controls 🔒

![68747470733a2f2f692e696d6775722e636f6d2f59514e613950702e6a7067](https://github.com/user-attachments/assets/0d896eda-1d4b-4191-a8c6-686c18cb8466)


	•	NSGs hardened (blocking all traffic except from my admin workstation)
	•	Built-in firewalls enabled on all VMs
	•	Private Endpoints applied to other resources

🌐 Attack Maps & Metrics

Before Hardening 🟥

**Start Time: 2024-09-25 10:07**\
**Stop Time: 2023-09-26 10:17**

![nsg-malicious-allowed-in(before)](https://github.com/user-attachments/assets/55769f24-8538-44dc-aa6e-1d10e17a9a51)

![linux-ssh-auth-fail(before)](https://github.com/user-attachments/assets/569b11cf-27b6-4280-88da-91d01dcd8b45)

![windows-rdp-auth-fail(before)](https://github.com/user-attachments/assets/a4f27df9-6cc4-44cc-8068-9691201f075a)

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 80,050
| Syslog                   | 8,248
| SecurityAlert            | 5
| SecurityIncident         | 175
| AzureNetworkAnalytics_CL | 3,312

After Hardening 🟩

**Start Time: 2024-10-03 15:07**\
**Stop Time: 2024-10-04 15:07**

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 17,467
| Syslog                   | 10
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

🚨 Attack Maps Before Hardening

	•	NSG Allowed Inbound Malicious Flows
	•	Linux Syslog Auth Failures
	•	Windows RDP/SMB Auth Failures

Post-hardening, there were no instances of malicious activity within the 24-hour period.

⚙️ Components

The architecture of the mini honeynet in Azure consists of the following components:

	•	Virtual Network (VNet)
	•	Network Security Group (NSG)
	•	Virtual Machines (2 Windows, 1 Linux)
	•	Log Analytics Workspace
	•	Azure Key Vault
	•	Azure Storage Account
	•	Microsoft Sentinel

📝 Conclusion

This project involved building a mini honeynet in Microsoft Azure, integrating logs into a Log Analytics workspace, and using Microsoft Sentinel for monitoring. After applying security controls, we observed a significant reduction in security incidents and malicious flows, demonstrating the effectiveness of the controls.

While the metrics after hardening showed fewer events, it’s important to consider that if the resources had been more actively used by regular users, more security events may have been generated.
