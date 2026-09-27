# Azure Home SOC Lab

A hands-on Security Operations Center (SOC) laboratory built in Microsoft Azure to demonstrate security monitoring, Windows security event collection, SIEM integration, KQL-based investigation, and authentication event analysis.

##  Project Overview

This project demonstrates the development of a small cloud-based SOC monitoring environment using Microsoft Azure.

A Windows virtual machine was deployed as the monitored host and configured to generate Windows security events. Microsoft Sentinel was then integrated with a Log Analytics Workspace to collect and analyze security-related events.

The project focuses on understanding how a SOC analyst can collect security telemetry, investigate authentication activity, identify potentially suspicious events, and use SIEM capabilities to support security monitoring.



##  Objectives

The main objectives of this project were to:

* Deploy a Windows virtual machine in Microsoft Azure.
* Configure an Azure Virtual Network and Network Security Group.
* Establish remote access to the Windows VM.
* Configure Windows security monitoring.
* Create an Azure Log Analytics Workspace.
* Deploy Microsoft Sentinel.
* Configure Windows Security Events collection.
* Create a Data Collection Rule.
* Query security events using KQL.
* Investigate authentication activity.
* Analyze failed and successful login events.
* Develop practical SOC monitoring and investigation skills.



## Architecture

The lab follows this general monitoring architecture:


                    INTERNET
                       │
                       ▼
              ┌─────────────────┐
              │  Azure Network  │
              │      / NSG      │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │  Windows VM     │
              │    Honeypot     │
              └────────┬────────┘
                       │
                Windows Security
                     Events
                       │
                       ▼
              ┌─────────────────┐
              │  Log Analytics  │
              │    Workspace    │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │    Microsoft    │
              │    Sentinel     │
              └─────────────────┘


### Architecture Diagram

![Azure SOC Architecture](architecture/architecture-diagram.png)



##  Technologies Used

| Technology              | Purpose                           |
| ----------------------- | --------------------------------- |
| Microsoft Azure         | Cloud infrastructure              |
| Azure Virtual Machine   | Monitored Windows host            |
| Azure Virtual Network   | Network connectivity              |
| Network Security Group  | Network access control            |
| Log Analytics Workspace | Security log storage and analysis |
| Microsoft Sentinel      | SIEM and security monitoring      |
| Windows Security Events | Security telemetry                |
| KQL                     | Security event investigation      |
| PowerShell              | Connectivity and system testing   |
| RDP                     | Remote administration             |



# Lab Implementation

## 1. Azure Resource Group

A dedicated Azure Resource Group was created to organize the resources used throughout the SOC laboratory.

The resources were maintained within the same Azure region to simplify deployment and management.

![Resource Group](screenshots/01-resource-group.png)



## 2. Azure Virtual Network

An Azure Virtual Network was created to provide network connectivity for the Windows virtual machine.

![Virtual Network](screenshots/02-virtual-network.png)



## 3. Windows Virtual Machine

A Windows virtual machine was deployed as the monitored host for the SOC laboratory.

The VM was configured within the same resource group and region as the supporting Azure resources.

![Virtual Machine](screenshots/03-virtual-machine.png)

---

## 4. Network Security Group

A Network Security Group was associated with the environment to control network traffic reaching the virtual machine.

![Network Security Group](screenshots/04-network-security-group.png)

---

## 5. Remote Desktop Access

Remote Desktop Protocol (RDP) was used to connect to the Windows virtual machine for configuration and testing.

![RDP Login](screenshots/05-rdp-login.png)

---

## 6. Windows Firewall Testing

The Windows Firewall configuration was examined as part of the laboratory's connectivity and monitoring experiment.

![Windows Firewall](screenshots/06-windows-firewall.png)

> **Note:** Firewall configuration changes were performed only within the controlled laboratory environment.

---

## 7. Connectivity Testing

Connectivity between the local system and Azure VM was tested using PowerShell.

![Connectivity Test](screenshots/07-connectivity-test.png)

---

# SIEM Deployment

## 8. Log Analytics Workspace

A Log Analytics Workspace was created to provide a central location for collecting and analyzing security-related telemetry.

![Log Analytics](screenshots/08-log-analytics.png)

---

## 9. Microsoft Sentinel

Microsoft Sentinel was enabled and connected to the Log Analytics Workspace.

![Microsoft Sentinel](screenshots/09-microsoft-sentinel.png)

---

## 10. Sentinel Content Hub

The Windows Security Events solution was installed through the Microsoft Sentinel Content Hub.

![Content Hub](screenshots/10-content-hub.png)

---

## 11. Security Events Connector

The Windows Security Events connector was configured to collect security events from the Windows environment.

![Security Events Connector](screenshots/11-security-events-connector.png)

---

## 12. Data Collection Rule

A Data Collection Rule was created to define the security events that would be collected.

The laboratory used the **All security events** option.

![Data Collection Rule](screenshots/12-data-collection-rule.png)



# Security Investigation

## 13. Security Events

After configuration, Windows security events began appearing in the Log Analytics environment.

![Security Events](screenshots/13-security-events.png)

The number of collected events increased over time, providing a larger dataset for investigation.



## 14. Failed Login Investigation

Authentication events were investigated to identify failed login activity.

![Failed Login Events](screenshots/14-failed-logins.png)

A KQL query was used to identify failed authentication events:

```kql
SecurityEvents
| where EventID == 4625
| sort by TimeGenerated desc


The investigation process included reviewing:

* Event timestamps
* Account names
* Source IP addresses where available
* Authentication activity
* Repeated failed login attempts
* Related successful authentication activity



## 15. Individual Event Analysis

Individual security events were examined to understand the available forensic information.

![Event Analysis](screenshots/15-event-analysis.png)

The collected events provided information such as account names, timestamps, IP addresses and activity associated with the events.



#  KQL Investigation

The repository contains additional KQL queries used during the investigation.

See:

[`queries/sentinel-kql-queries.md`](queries/sentinel-kql-queries.md)

Example:

```kql
SecurityEvents
| where TimeGenerated > ago(24h)
| sort by TimeGenerated desc
```

### Failed Authentication Events

```kql
SecurityEvents
| where EventID == 4625
| sort by TimeGenerated desc


### Successful Authentication Events

```kql
SecurityEvents
| where EventID == 4624
| sort by TimeGenerated desc




# Investigation Workflow

The investigation followed a basic SOC workflow:


Collect
   ↓
Centralize
   ↓
Query
   ↓
Identify
   ↓
Investigate
   ↓
Document


### Collect

Windows security events were collected from the monitored VM.

### Centralize

Events were sent to the Log Analytics Workspace.

### Monitor

Microsoft Sentinel provided the SIEM environment for security monitoring.

### Query

KQL was used to search and filter security events.

### Investigate

Authentication events were examined for failed and successful login activity.

### Document

The investigation process and findings were documented for future analysis.

---

#  Key Findings

The laboratory demonstrated that:

* Windows security events can be centrally collected in Azure.
* Microsoft Sentinel can provide a centralized environment for security monitoring.
* Authentication events can be queried using KQL.
* Security events provide useful information such as timestamps, accounts and IP addresses.
* Increasing event volume provides a larger dataset for security investigation.
* Individual security events can provide useful context for understanding authentication activity.

---

# Security Considerations

The laboratory also demonstrates the importance of carefully controlling exposed services and monitoring authentication activity.

In a production environment, additional controls would be required, including:

* Restricting administrative access.
* Implementing least privilege.
* Using strong authentication controls.
* Monitoring exposed services.
* Creating automated detection rules.
* Configuring alerts for suspicious activity.
* Regularly reviewing security logs.
* Protecting credentials and secrets.

---

# Skills Demonstrated

This project demonstrates practical experience with:

### Cloud Security

* Microsoft Azure
* Azure networking
* Virtual machine deployment
* Network Security Groups

### SOC Operations

* Security monitoring
* Log collection
* SIEM configuration
* Event investigation
* Authentication monitoring

### Security Tools

* Microsoft Sentinel
* Log Analytics
* Windows Security Events
* PowerShell

### Security Analysis

* KQL
* Event filtering
* Authentication analysis
* IP address analysis
* Timeline analysis

---

# Repository Structure


azure-home-soc-lab/
│
├── README.md
├── architecture/
│   └── architecture-diagram.png
│
├── screenshots/
│   ├── 01-resource-group.png
│   ├── 02-virtual-network.png
│   ├── 03-virtual-machine.png
│   ├── 04-network-security-group.png
│   ├── 05-rdp-login.png
│   ├── 06-windows-firewall.png
│   ├── 07-connectivity-test.png
│   ├── 08-log-analytics.png
│   ├── 09-microsoft-sentinel.png
│   ├── 10-content-hub.png
│   ├── 11-security-events-connector.png
│   ├── 12-data-collection-rule.png
│   ├── 13-security-events.png
│   ├── 14-failed-logins.png
│   └── 15-event-analysis.png
│
├── queries/
│   └── sentinel-kql-queries.md
│
├── investigation/
│   └── failed-login-investigation.md
│
├── documentation/
│   └── azure-soc-lab-report.pdf
│
└── .gitignore


---

#  Documentation

The complete laboratory report is available here:

[`Azure SOC Lab Report`](documentation/azure-soc-lab-report.pdf)

Additional investigation material and KQL queries are available in their respective repository directories.



#  Disclaimer

This project was created for educational and cybersecurity laboratory purposes.

All testing and configuration activities were performed within a controlled laboratory environment.

No unauthorized systems were intentionally targeted.



