# Home Lab: Azure VM Exposed to Global Attacks

---

This home lab project demonstrates how to deploy an Azure Virtual Machine exposed to the internet to attract attackers from around the world. We will use Azure Log Analytics Workspace and Security Information and Event Management (SIEM) tools to monitor malicious activity and analyze the incoming attack vectors in real-time.

---

## Table of Contents
- [About the Project](#about-the-project)
- [Architecture Overview](#architecture-overview)
- [Lab Setup](#lab-setup)
- [Monitoring and Analysis Tools](#monitoring-and-analysis-tools)
- [Installation](#installation)
- [Usage](#usage)
- [Screenshots](#screenshots)
- [Contributing](#contributing)
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

## Architecture Overview

The architecture consists of the following components:
1. **Azure VM**: A virtual machine running Ubuntu, exposed to the internet via a public IP, with minimal security to invite potential attacks.
2. **Log Analytics Workspace**: An Azure service used to collect, analyze, and monitor log data from the VM.
3. **SIEM Tool (Azure Sentinel or another third-party solution)**: Integrated with Log Analytics Workspace to track and correlate security events.
4. **Attack Traffic**: Traffic from global attackers targeting the open VM.

---

## Lab Setup

### Prerequisites:
- An active [Microsoft Azure](https://azure.microsoft.com) account.
- Basic knowledge of Azure resources and networking.
- Access to an Azure Subscription that allows resource deployment.
- A Security Information and Event Management (SIEM) tool (e.g., Azure Sentinel, Splunk, etc.).

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

## Monitoring and Analysis Tools

### Azure Log Analytics
- **Logs Captured**: 
  - Syslog
  - Performance logs
  - Security events (failed SSH attempts, brute-force attacks, etc.)
  
- **Queries**: Use Kusto Query Language (KQL) to query and analyze the logs. Example query to view failed SSH login attempts:
  ```kusto
  Syslog
  | where Facility == "auth"
  | where SeverityLevel == "Error"
  | where ProcessName == "sshd"
  | project TimeGenerated, Computer, UserName, Message
  ```

### SIEM (Azure Sentinel or other)
- **Dashboards**: Use predefined or custom dashboards to visualize attack patterns.
- **Alerts**: Set up rules to trigger alerts for suspicious behavior (e.g., repeated failed login attempts).
  
---

## Installation

### Step-by-Step Guide

1. **Clone the Repository** (if hosting lab files, scripts, etc.):
   ```bash
   git clone https://github.com/username/azure-vm-security-lab.git
   cd azure-vm-security-lab
   ```

2. **Deploy the Azure VM**:
   Follow the instructions to deploy the VM using the provided ARM templates or manual setup guide.

3. **Connect VM to Log Analytics**:
   - Use the Azure Portal or the Azure CLI to link your VM to the Log Analytics Workspace.
   - Install the Azure Monitoring Agent on your VM:
   ```bash
   wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh
   sudo bash onboard_agent.sh -w <WorkspaceID> -s <SharedKey>
   ```

4. **Configure SIEM Tool**:
   - Set up your SIEM tool to monitor data from Log Analytics.

---

## Usage

- The VM will start capturing traffic as soon as it's deployed and exposed to the internet.
- Use Azure Log Analytics or the SIEM platform to monitor:
  - Failed SSH login attempts
  - Web exploit attempts (if a web service is running)
  - Network scans and enumeration attempts
  
- Analyze attack vectors using SIEM dashboards and respond to any detected threats with custom queries or automated playbooks.

Example of a KQL query to track incoming brute-force attacks:
```kusto
SecurityEvent
| where EventID == 4625
| summarize count() by IpAddress, Computer
| order by count_ desc
```

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

Your Name - [@YourTwitterHandle](https://twitter.com/YourTwitterHandle) - email@example.com

Project Link: [https://github.com/username/azure-vm-security-lab](https://github.com/username/azure-vm-security-lab)

---

## Acknowledgements

- [Azure Log Analytics Documentation](https://docs.microsoft.com/en-us/azure/azure-monitor/logs/log-analytics-workspace-overview)
- [Azure Sentinel](https://docs.microsoft.com/en-us/azure/sentinel/)
- [Kusto Query Language (KQL) Reference](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/query/)

---

This template should help you set up and monitor your Azure VM lab for cybersecurity purposes effectively. Let me know if you need any further modifications!
