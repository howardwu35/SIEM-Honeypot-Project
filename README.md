# Home Lab: Azure VM Exposed to Global Attacks

---

This project provides a comprehensive walkthrough of using Microsoft Azure to deploy a Windows 10 virtual machine (VM) in the cloud, configured for internet accessibility. The setup employs Azure Log Analytics Workspace, Microsoft Defender for Cloud, and Microsoft Sentinel to collect, aggregate, and visualize security-related data. Specifically, PowerShell is used to monitor Event Viewer on the exposed VM, focusing on EventID 4625, which tracks failed logon attempts. This log data is directed to a logfile, and the PowerShell script sends the IP addresses of failed logons to IPgeolocation.io via an API. The geolocation data is then utilized in Microsoft Sentinel to map the origins of these login attempts, enhancing security visibility. This project illustrates effective use of Azure’s cloud security and monitoring tools for real-time threat detection and analysis.

---

## Table of Contents
- [About the Project](#about-the-project)
- [Tools and Environments Used](#tools-and-environments-used) 
- [Architecture Overview](#architecture-overview)
- [Lab Setup](#lab-setup)
- [Usage](#usage)
- [Screenshots](#screenshots)
- [License](#license)
- [Contact](#contact)

---

## About the Project

This home lab allows us to simulate real-world attacks on a deliberately exposed Azure Virtual Machine (VM) by setting up a vulnerable environment. The purpose is to study attack patterns, gather threat intelligence, and gain hands-on experience with cybersecurity monitoring tools like Azure Log Analytics and a SIEM platform. 

We intentionally expose the VM to the internet and track the malicious activities using the following:
- Azure Log Analytics Workspace to capture logs.
- A Security Information and Event Management (SIEM) tool to correlate, visualize, and alert on attack patterns.
  
The data collected is used for forensic analysis, intrusion detection, and crafting better defensive mechanisms.

---

## Tools and Environments Used

- **Microsoft Azure**: Cloud platform for hosting and managing resources.
  - **Azure Virtual Machines**: Windows 10 VM deployed as a monitored target.
  - **Azure Log Analytics Workspace**: Centralized tool for log collection and data analysis.
  - **Microsoft Defender for Cloud**: Advanced threat protection and security insights.
  - **Microsoft Sentinel**: SIEM (Security Information and Event Management) tool for aggregating and visualizing security events.

- **PowerShell**: Scripting language used for automation, particularly for monitoring Event Viewer on the VM and logging failed login attempts.

- **IPgeolocation API** (via [IPgeolocation.io](https://ipgeolocation.io/)): API to fetch geolocation data based on IP addresses, enabling mapping of login attempt origins in Microsoft Sentinel.

- **Windows Event Viewer**: Integrated tool on Windows 10 VM used for system and security event logging, with a focus on EventID 4625 for tracking failed login attempts.

---

## Architecture Overview

The architecture consists of the following components:
1. **Azure VM**: A virtual machine running Ubuntu, exposed to the internet via a public IP, with minimal security to invite potential attacks.
2. **Log Analytics Workspace**: An Azure service used to collect, analyze, and monitor log data from the VM.
3. **SIEM Tool (Azure Sentinel or another third-party solution)**: Integrated with Log Analytics Workspace to track and correlate security events.
4. **Attack Traffic**: Traffic from global attackers targeting the open VM.

| ![Alt text](images/SIEM_Lab_Architecture.jpg) |
|:------------------------------:|

---

## Lab Setup

### Prerequisites:
- An active [Microsoft Azure](https://azure.microsoft.com) account.
- Windows Machine (This project is tailored towards Windows OS)
  - PowerShell Installed
- Internet Access 

### Steps:

1. **Create the Azure VM**:
   - Deploy a Linux VM (e.g., Ubuntu) using the Azure Portal.
   - Ensure the VM has a public IP address and is connected to the internet with minimal firewall protections.
   - Open necessary ports to attract attacks (e.g., SSH on port 22, HTTP on port 80, etc.).

2. **Set Up Log Analytics Workspace**:
   - In the Azure Portal, create a Log Analytics Workspace.
   - Link the VM to this workspace to start collecting logs (e.g., security events, syslog, network data).

3. **Configure SIEM Tool**:
   - Deploy and integrate a SIEM tool like Azure Sentinel or another tool.
   - Connect it to your Log Analytics Workspace for real-time monitoring and alerts.
   - Set up workbooks and detection rules to analyze malicious activity.

4. **Expose VM**:
   - Leave the VM running continuously to attract global attackers.
   - Monitor and capture the attack traffic.

---

## Usage

- The VM will start capturing traffic as soon as it's deployed and exposed to the internet.
- Use Azure Log Analytics or the SIEM platform to monitor:
  - Failed RDP login attempts
  
- Analyze attack vectors using SIEM dashboards and respond to any detected threats with custom queries or automated playbooks.

---

## Screenshots

![VM Log Analytics Dashboard](link-to-dashboard-image.png)

![SIEM Attack Analysis](link-to-siem-analysis-image.png)

---

## Contributing

Feel free to contribute by opening an issue or submitting a pull request.

1. Fork the project.
2. Create your feature branch (`git checkout -b feature/AmazingFeature`).
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`).
4. Push to the branch (`git push origin feature/AmazingFeature`).
5. Open a pull request.

---

## License

Distributed under the MIT License. See `LICENSE` for more information.

---

## Contact

Howard Wu - howardwu35@gmail.com

Project Link: [https://github.com/username/azure-vm-security-lab](https://github.com/username/azure-vm-security-lab)

---

## Acknowledgements

- [Azure Log Analytics Documentation](https://docs.microsoft.com/en-us/azure/azure-monitor/logs/log-analytics-workspace-overview)
- [Azure Sentinel](https://docs.microsoft.com/en-us/azure/sentinel/)
- [Kusto Query Language (KQL) Reference](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/query/)

