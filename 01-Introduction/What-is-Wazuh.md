# What is Wazuh?

## Overview

Wazuh is an open-source cybersecurity platform that combines **Security Information and Event Management (SIEM)** and **Extended Detection and Response (XDR)** capabilities into a single solution.

It enables organizations to collect, analyze, correlate, and respond to security events across endpoints, servers, cloud environments, containers, virtual machines, and network devices from a centralized platform.

By continuously monitoring systems for suspicious activity, configuration weaknesses, file modifications, vulnerabilities, and other security events, Wazuh helps organizations improve their overall security posture while simplifying security operations.

---

# Why Was Wazuh Created?

Modern IT infrastructures generate enormous volumes of logs and security events every day.

Without centralized monitoring, security teams would have to manually inspect logs from individual servers, workstations, applications, firewalls, and cloud services, making it difficult to detect attacks quickly.

Wazuh addresses these challenges by providing:

- Centralized security monitoring
- Continuous endpoint visibility
- Threat detection
- Automated alerting
- Incident response
- Compliance monitoring
- Vulnerability assessment

Instead of reviewing thousands of separate log files, analysts can monitor their entire infrastructure through a single platform.

---

# Wazuh as a SIEM and XDR Platform

Wazuh combines capabilities traditionally found in both **SIEM** and **XDR** platforms.

## SIEM

As a SIEM platform, Wazuh provides:

- Centralized log collection
- Log analysis
- Event correlation
- Alert generation
- Threat monitoring
- Incident investigation
- Compliance reporting

Its SIEM functionality allows security teams to collect and analyze security events from many different sources through a centralized platform.

## XDR

Beyond log management, Wazuh extends visibility directly to monitored endpoints.

Its XDR capabilities include:

- File Integrity Monitoring (FIM)
- Vulnerability Detection
- Security Configuration Assessment (SCA)
- Rootcheck
- Active Response
- Endpoint Inventory

These capabilities allow Wazuh not only to detect security events but also to monitor endpoint health, identify vulnerabilities, enforce security baselines, and automatically respond to certain threats.

---

# Key Features

Some of Wazuh's major capabilities include:

- Centralized Log Collection
- Threat Detection
- Event Correlation
- Endpoint Monitoring
- Vulnerability Detection
- File Integrity Monitoring (FIM)
- Security Configuration Assessment (SCA)
- Active Response
- Rootcheck
- Endpoint Inventory
- Compliance Monitoring
- Cloud Monitoring
- Container Security

---

# Where Can Wazuh Monitor?

Wazuh supports monitoring across a wide variety of environments.

These include:

- Windows
- Linux
- macOS
- Docker
- Kubernetes
- AWS
- Microsoft Azure
- Google Cloud Platform (GCP)
- Virtual Machines
- Network Devices
- Syslog-enabled appliances

This flexibility allows organizations to monitor hybrid environments from a single management platform.

---

# Deployment Models

Wazuh supports two primary monitoring methods.

## Agent-Based Monitoring

The preferred deployment model.

A lightweight **Wazuh Agent** is installed on monitored systems to continuously collect security events and send them securely to the Wazuh Manager.

Agent-based monitoring provides the deepest visibility and supports advanced capabilities such as:

- File Integrity Monitoring
- Vulnerability Detection
- Active Response
- Security Configuration Assessment
- Endpoint Inventory

---

## Agentless Monitoring

Some systems cannot run additional software.

For these systems, Wazuh supports **Agentless Monitoring**, where the Wazuh Manager remotely collects information using technologies such as:

- SSH
- Syslog

Although this provides useful visibility, it offers fewer capabilities than agent-based monitoring because the Manager does not have direct access to the operating system.

---

# High-Level Architecture

Every Wazuh deployment is built around four primary components.

| Component | Purpose |
|------------|---------|
| **Manager** | Collects and analyzes security events. |
| **Agent** | Collects data from monitored endpoints. |
| **Indexer** | Stores and indexes alerts. |
| **Dashboard** | Web interface used to visualize and manage alerts. |

> **Note**
>
> Some older Wazuh deployments also include **Filebeat** as a supporting component for forwarding alerts between the Manager and the Indexer. Modern Wazuh documentation (4.8+) focuses on the four primary components listed above.

A more detailed explanation of these components is provided in the **Core Components** section of this knowledge base.

---

# How Wazuh Works (High-Level)

The overall workflow can be summarized as:

```text
Security Event
      │
      ▼
 Agent / SSH / Syslog
      │
      ▼
 Wazuh Manager
      │
      ▼
 Decoders & Rules
      │
      ▼
 Alert Generated
      │
      ▼
 Wazuh Indexer
      │
      ▼
 Wazuh Dashboard
      │
      ▼
 Security Analyst
```

The detailed event processing workflow is covered separately in **Wazuh-Workflow.md**.

---

# Real-World Example

An employee accidentally downloads malware onto a Windows workstation.

1. The Wazuh Agent detects that a protected file has been modified.
2. The event is securely transmitted to the Wazuh Manager.
3. The Manager analyzes the event using Decoders and Rules.
4. An alert is generated.
5. The alert is stored in the Wazuh Indexer.
6. The Dashboard displays the alert.
7. A security analyst investigates the affected system and determines the appropriate response.

---

# What You'll Learn Next

This document provides a high-level introduction to Wazuh.

The following documents explore each topic in greater detail:

- What is SIEM?
- What is XDR?
- Wazuh Architecture
- Wazuh Workflow
- Wazuh Manager
- Wazuh Agent
- Wazuh Indexer
- Wazuh Dashboard
- Decoders
- Rules

---

## Key Takeaways

- Wazuh is an open-source SIEM and XDR platform.
- It centralizes security monitoring across diverse environments.
- It supports both agent-based and agentless monitoring.
- Its architecture is built around four primary components: Manager, Agent, Indexer, and Dashboard.
- Wazuh transforms raw security events into actionable alerts that help security teams detect, investigate, and respond to threats.

---

## References

- Wazuh Documentation – Getting Started  
  https://documentation.wazuh.com/current/getting-started/index.html

- Wazuh Documentation – Architecture  
  https://documentation.wazuh.com/current/getting-started/architecture.html

- Wazuh Documentation – Components  
  https://documentation.wazuh.com/current/getting-started/components/index.html
