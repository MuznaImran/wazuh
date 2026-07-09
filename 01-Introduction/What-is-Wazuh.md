# What is Wazuh?

## Overview

Wazuh is an open-source cybersecurity platform that provides **Security Information and Event Management (SIEM)** and **Extended Detection and Response (XDR)** capabilities. It enables organizations to monitor endpoints, collect and analyze security events, detect threats, assess vulnerabilities, enforce security policies, and respond to incidents from a centralized platform.

Wazuh continuously collects and analyzes security events from endpoints, servers, cloud environments, containers, network devices, and applications. It processes this information using built-in and custom decoders and detection rules, generating actionable alerts that are presented through a centralized dashboard.

Because Wazuh is open source, organizations can deploy enterprise-grade security monitoring without expensive licensing costs while maintaining flexibility, transparency, and customization.

---

# What Problems Does Wazuh Solve?

Modern organizations operate hundreds or even thousands of systems, each generating security logs and events.

Without a centralized platform, security teams would need to manually inspect logs from every server, workstation, firewall, application, and network device, making threat detection slow and inefficient.

Wazuh addresses this challenge by:

- Collecting logs from multiple sources
- Normalizing and analyzing security events
- Detecting suspicious behavior
- Generating security alerts
- Supporting automated incident response
- Providing centralized visibility across the infrastructure

---

# Wazuh as a SIEM and XDR Platform

Wazuh combines the capabilities of both a **Security Information and Event Management (SIEM)** platform and an **Extended Detection and Response (XDR)** platform.

## SIEM Capabilities

As a SIEM, Wazuh focuses on collecting, storing, analyzing, and correlating security events from across an organization's infrastructure.

Its SIEM capabilities include:

- Centralized log collection
- Event correlation
- Security alert generation
- Log storage and indexing
- Threat monitoring
- Incident investigation
- Compliance reporting

These capabilities provide security teams with centralized visibility into their organization's security posture.

---

## XDR Capabilities

Beyond traditional SIEM functionality, Wazuh also provides several XDR capabilities that improve endpoint visibility and automate threat detection and response.

### File Integrity Monitoring (FIM)

Monitors important files and directories for unauthorized modifications.

### Vulnerability Detection

Identifies vulnerable software installed on monitored endpoints using continuously updated vulnerability databases.

### Security Configuration Assessment (SCA)

Evaluates operating systems and applications against security best practices and compliance frameworks.

### Rootcheck

Detects indicators of rootkits, hidden processes, suspicious files, and other signs of system compromise.

### Active Response

Automatically executes predefined actions—such as blocking an IP address or terminating a malicious process—when specific security rules are triggered.

### Endpoint Inventory

Collects detailed information about hardware, installed software, operating systems, running processes, network interfaces, and open ports.

These capabilities allow Wazuh to move beyond traditional log management and provide comprehensive endpoint detection and response.

---

# Key Features

Wazuh provides a comprehensive set of security capabilities that can be grouped into three categories:

- **SIEM** – Centralized log collection, event correlation, alerting, and incident investigation.
- **XDR** – Endpoint monitoring, threat detection, vulnerability assessment, File Integrity Monitoring (FIM), Security Configuration Assessment (SCA), Rootcheck, and Active Response.
- **Infrastructure Monitoring** – Monitoring of endpoints, cloud workloads, containers, and selected network devices through agent-based and agentless monitoring.

The following section explores Wazuh's SIEM and XDR capabilities in more detail.

---

# Core Components

To provide these capabilities, Wazuh is built using several core components that work together to collect, analyze, store, and visualize security events.
A standard Wazuh deployment consists of four primary components.

| Component | Purpose |
|-----------|---------|
| **Wazuh Manager (Server)** | Receives events from agents, analyzes logs using decoders and rules, generates alerts, and coordinates security monitoring. |
| **Wazuh Agent** | Installed on monitored endpoints to collect logs, file changes, system information, vulnerabilities, and security events. |
| **Wazuh Indexer** | Stores and indexes alerts and events, allowing fast searches and efficient data retrieval. |
| **Wazuh Dashboard** | Provides the web interface used to visualize alerts, investigate incidents, manage agents, and administer the platform. |

> **Note**
>
> Small environments typically deploy a single Wazuh Manager. Larger enterprise environments may deploy multiple Managers in a cluster to provide scalability, high availability, and fault tolerance.

---

# Supporting Components

In addition to its core components, some Wazuh deployments include supporting services that facilitate data transfer and integration between components.

## Filebeat

**Filebeat** is a lightweight log shipper developed by Elastic. In Wazuh deployments, it is used to forward alerts and events generated by the **Wazuh Manager** to the **Wazuh Indexer**, where they are stored, indexed, and made searchable through the Wazuh Dashboard.

```
Agent
   │
   ▼
Manager
   │
   ▼
Filebeat
   │
   ▼
Indexer
   │
   ▼
Dashboard
```

Although Filebeat does not perform security analysis or threat detection, it plays an important role in transporting alert data between components in many Wazuh deployments.

### Version Notes

> **Older Wazuh Releases**
>
> Earlier Wazuh deployments used **Elasticsearch** as the backend for storing and indexing alerts. In these deployments, **Filebeat** acted as the log shipper responsible for forwarding alerts from the Wazuh Manager to Elasticsearch. As a result, many architecture diagrams and tutorials included Filebeat as one of the primary components.

> **Modern Wazuh Documentation (4.8+ Releases)**
>
> The official documentation for modern Wazuh releases emphasizes four primary architectural components:
>
> - Wazuh Manager
> - Wazuh Agent
> - Wazuh Indexer
> - Wazuh Dashboard
>
> Although Filebeat is no longer highlighted as a primary architectural component, it is **not obsolete**. It continues to be used in many production deployments, migration scenarios, upgrades, and environments originally built using earlier Wazuh releases.

### Why the Change?

Wazuh gradually transitioned away from relying on Elastic's ecosystem by adopting the **Wazuh Indexer**, which is based on **OpenSearch**, as its official indexing and search engine.

This simplified the platform architecture and allowed the official documentation to focus on the four core components while treating Filebeat as a supporting service rather than a fundamental architectural component.

---

# Overall Architecture

A typical Wazuh deployment consists of four primary components that work together to collect, analyze, store, and visualize security events.

```text
               +----------------------+
               |   Monitored Systems  |
               | (Endpoints, Servers, |
               | Cloud, Containers)   |
               +----------+-----------+
                          │
                 Agent / SSH / Syslog
                          │
                          ▼
               +----------------------+
               |    Wazuh Manager     |
               | Decoders & Rules     |
               +----------+-----------+
                          │
                 Alerts Generated
                          │
                          ▼
               +----------------------+
               |    Wazuh Indexer     |
               | Store & Search Data  |
               +----------+-----------+
                          │
                          ▼
               +----------------------+
               |   Wazuh Dashboard    |
               | Visualize & Manage   |
               +----------+-----------+
                          │
                          ▼
                  Security Analysts
```

---

# Decoders and Rules

The Wazuh Manager processes incoming events using two important mechanisms:

## Decoders

Decoders parse raw log data received from agents or external devices. They extract useful information such as usernames, IP addresses, event IDs, file names, timestamps, and process names, converting unstructured logs into a standardized format.

## Rules

Once an event has been decoded, it is evaluated against Wazuh's predefined and custom detection rules.

Rules determine:

- Whether the event is suspicious
- The severity of the event
- The alert level
- Whether Active Response should be triggered

Each generated alert is assigned a severity level that helps security analysts prioritize their investigations. Higher alert levels generally indicate events that require more immediate attention.

Together, decoders and rules allow Wazuh to transform raw log data into meaningful security alerts.

---

# Agent-Based Monitoring

A **Wazuh Agent** is lightweight software installed on an endpoint that continuously monitors the system, performs local security checks, and securely sends security events to the **Wazuh Manager** for analysis.

Communication between the Wazuh Agent and the Wazuh Manager is encrypted and authenticated to ensure the confidentiality and integrity of transmitted security data.

The agent collects a wide range of security-related information, including:

- System logs
- Authentication events
- Running processes
- Installed software
- File modifications
- Vulnerability information
- System inventory
- Security configuration data

Supported operating systems include:

- Windows
- Linux
- macOS
- Solaris
- AIX

Because the agent runs directly on the monitored endpoint, it provides deep visibility into system activity and enables advanced monitoring capabilities such as:

- File Integrity Monitoring (FIM)
- Vulnerability Detection
- Security Configuration Assessment (SCA)
- Rootcheck
- Active Response
- Endpoint Inventory

## How It Works

The following diagram illustrates the flow of security events in an **agent-based** Wazuh deployment.

```text
+-------------------------+
| Security Event Occurs   |
| (e.g., login, file      |
| change, new process)    |
+-------------------------+
            │
            ▼
+-------------------------+
| Wazuh Agent             |
| Collects event data     |
+-------------------------+
            │
            │ Secure communication
            │ (Encrypted)
            ▼
+-------------------------+
| Wazuh Manager           |
| Receives the event      |
+-------------------------+
            │
            ▼
+-------------------------+
| Decoders                |
| Parse & normalize logs  |
+-------------------------+
            │
            ▼
+-------------------------+
| Rules Engine            |
| Evaluates the event     |
+-------------------------+
            │
            ▼
+-------------------------+
| Alert Generated         |
+-------------------------+
            │
            ▼
+-------------------------+
| Wazuh Indexer           |
| Stores & indexes data   |
+-------------------------+
            │
            ▼
+-------------------------+
| Wazuh Dashboard         |
| Displays alerts         |
+-------------------------+
            │
            ▼
+-------------------------+
| Security Analyst        |
| Investigates alert      |
+-------------------------+
```

### Workflow Summary

1. A security event occurs on a monitored endpoint.
2. The **Wazuh Agent** detects and collects information about the event.
3. The agent securely forwards the event to the **Wazuh Manager**.
4. The Manager uses **Decoders** to parse and normalize the incoming data.
5. The **Rules Engine** evaluates the event against predefined and custom detection rules.
6. If a rule is matched, an alert is generated.
7. The alert is forwarded to the **Wazuh Indexer**, where it is stored and indexed.
8. The **Wazuh Dashboard** retrieves the alert from the Indexer and displays it.
9. A **Security Analyst** reviews the alert, investigates the event, and determines the appropriate response.
    
---

# Agentless Monitoring

Although **agent-based monitoring** is the preferred method in Wazuh, some systems do not allow third-party software to be installed or are not compatible with the Wazuh Agent.

Examples include:

- Network switches
- Routers
- Firewalls
- Legacy servers
- Embedded devices
- Third-party appliances

For these systems, Wazuh provides **Agentless Monitoring**, allowing the **Wazuh Manager** to collect security information remotely without installing an agent on the monitored device.

Depending on the device and configuration, the Manager can collect data using protocols such as:

- SSH
- Syslog

Unlike agent-based monitoring, the Manager does not have direct access to the operating system. Instead, it retrieves logs or command output remotely for analysis.

Because no agent is installed, agentless monitoring offers fewer capabilities than agent-based monitoring. Features such as:

- File Integrity Monitoring (FIM)
- Vulnerability Detection
- Security Configuration Assessment (SCA)
- Rootcheck
- Endpoint Inventory
- Active Response

are generally unavailable or significantly limited.

For this reason, organizations typically use **agent-based monitoring whenever possible**, reserving agentless monitoring for systems where installing an agent is impractical or unsupported.

## How It Works

The following diagram illustrates the flow of security events in an **agentless** Wazuh deployment.

```text
+---------------------------+
| Security Event Occurs     |
| (Router, Firewall, etc.)  |
+---------------------------+
             │
             ▼
+---------------------------+
| SSH / Syslog              |
| Remote data collection    |
+---------------------------+
             │
             ▼
+---------------------------+
| Wazuh Manager             |
| Receives logs/events      |
+---------------------------+
             │
             ▼
+---------------------------+
| Decoders                  |
| Parse & normalize logs    |
+---------------------------+
             │
             ▼
+---------------------------+
| Rules Engine              |
| Evaluates the event       |
+---------------------------+
             │
             ▼
+---------------------------+
| Alert Generated           |
+---------------------------+
             │
             ▼
+---------------------------+
| Wazuh Indexer             |
| Stores & indexes data     |
+---------------------------+
             │
             ▼
+---------------------------+
| Wazuh Dashboard           |
| Displays alerts           |
+---------------------------+
             │
             ▼
+---------------------------+
| Security Analyst          |
| Investigates alert        |
+---------------------------+
```

### Workflow Summary

1. A security event occurs on a device that cannot run a Wazuh Agent.
2. The **Wazuh Manager** remotely collects logs or command output using **SSH** or receives logs through **Syslog**.
3. The Manager receives the collected data.
4. **Decoders** parse and normalize the incoming information.
5. The **Rules Engine** evaluates the event against predefined and custom detection rules.
6. If a rule is matched, an alert is generated.
7. The alert is stored and indexed by the **Wazuh Indexer**.
8. The **Wazuh Dashboard** retrieves the alert from the Indexer and displays it.
9. A **Security Analyst** reviews the alert and investigates the event.

---

# Real-World Example

Consider a Windows workstation protected by Wazuh.

1. A user unknowingly downloads malicious software.
2. The malware modifies a protected system file.
3. The Wazuh Agent detects the file modification through **File Integrity Monitoring (FIM)**.
4. The Agent securely forwards the event to the Wazuh Manager.
5. The Manager decodes and normalizes the event.
6. The Rules Engine evaluates the event against its detection rules.
7. A rule identifying unauthorized system file modifications is matched.
8. An alert is generated and stored in the Wazuh Indexer.
9. The Wazuh Dashboard displays the alert to the Security Analyst.
10. The analyst investigates the endpoint and takes the appropriate response.

This example demonstrates how the Wazuh Agent, Manager, Decoders, Rules Engine, Indexer, and Dashboard work together to detect and investigate potential security threats.

---

## Key Takeaways

- Wazuh is an open-source cybersecurity platform that combines **SIEM** and **XDR** capabilities.
- It centralizes security monitoring across endpoints, servers, cloud environments, containers, and network devices.
- Its four primary components are the **Manager**, **Agent**, **Indexer**, and **Dashboard**.
- Supporting services such as **Filebeat** may still be encountered in existing deployments, although modern Wazuh documentation emphasizes the four core components.
- The **Manager** analyzes incoming events using **Decoders** and **Rules**, transforming raw logs into actionable security alerts.
- Wazuh supports both **agent-based** and **agentless** monitoring, allowing organizations to monitor a wide variety of devices.
- Features such as **File Integrity Monitoring**, **Vulnerability Detection**, **Security Configuration Assessment**, **Rootcheck**, and **Active Response** extend Wazuh beyond traditional SIEM functionality into a comprehensive XDR platform.

---

## References

- Wazuh Documentation – Getting Started  
  https://documentation.wazuh.com/current/getting-started/index.html

- Wazuh Documentation – Architecture  
  https://documentation.wazuh.com/current/getting-started/architecture.html

- Wazuh Documentation – Components  
  https://documentation.wazuh.com/current/getting-started/components/index.html

- Wazuh Documentation – Agents  
  https://documentation.wazuh.com/current/user-manual/agents/index.html

- Wazuh Documentation – Ruleset  
  https://documentation.wazuh.com/current/user-manual/ruleset/index.html

- Wazuh Documentation – Active Response  
  https://documentation.wazuh.com/current/user-manual/capabilities/active-response/index.html
