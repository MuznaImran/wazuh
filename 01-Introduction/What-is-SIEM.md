# What is SIEM?

## Overview

**Security Information and Event Management (SIEM)** is a cybersecurity solution that collects, stores, analyzes, and correlates security events and log data from multiple systems across an organization's infrastructure. Its primary purpose is to provide centralized visibility into security events, enabling security teams to detect threats, investigate incidents, and support regulatory compliance.

Instead of monitoring each device individually, a SIEM aggregates logs from multiple sources into a single platform where they can be searched, analyzed, and correlated to identify suspicious activity.

---

# Why Does SIEM Exist?

Every system in an organization generates logs.

Examples include:

- Windows Event Logs
- Linux Syslog
- Firewalls
- Routers and Switches
- Web Servers
- Databases
- Cloud Services
- Authentication Systems
- Applications

Without a SIEM, security analysts would need to manually inspect logs from each system separately, making threat detection slow and inefficient.

A SIEM centralizes these logs, making security monitoring significantly more effective.

---

# Core Functions of a SIEM

## Log Collection

Collects security events and logs from endpoints, servers, applications, network devices, cloud services, and security appliances.

Examples include:

- Windows Event Logs
- Linux Syslog
- Firewall Logs
- Authentication Logs
- Web Server Logs

---

## Log Normalization

Every device produces logs in a different format.

A SIEM converts these logs into a standardized format so they can be analyzed consistently regardless of their source.

---

## Log Storage

Stores collected logs for future investigations, auditing, compliance, and forensic analysis.

Depending on organizational requirements, logs may be retained for months or even years.

---

## Event Correlation

One of the most important capabilities of a SIEM is **event correlation**.

Instead of analyzing each event independently, the SIEM combines related events from multiple systems to detect suspicious patterns.

Example:

```
Multiple Failed Logins
        +
Successful Login
        +
Privilege Escalation
        +
Sensitive File Access
        =
Possible Account Compromise
```

This allows security analysts to detect attacks that individual events alone would not reveal.

---

## Alert Generation

When predefined or custom detection rules are matched, the SIEM generates alerts.

Examples include:

- Brute-force attacks
- Malware detection
- Privilege escalation
- Unauthorized access
- Suspicious process execution
- Policy violations

---

## Security Monitoring

A SIEM continuously monitors an organization's infrastructure and provides real-time visibility into security events, allowing analysts to quickly identify and investigate threats.

---

# How SIEM Works

The general workflow of a SIEM can be summarized as follows:

```
Endpoints
Servers
Firewalls
Applications
Cloud Services
        │
        ▼
 Log Collection
        │
        ▼
 Log Normalization
        │
        ▼
 Event Correlation
        │
        ▼
 Alert Generation
        │
        ▼
 SIEM Dashboard
        │
        ▼
 Security Analyst
```

---

# Common Use Cases

Organizations use SIEM platforms for:

- Security Operations Centers (SOC)
- Threat Detection
- Incident Response
- Threat Hunting
- Compliance Monitoring
- Security Auditing
- Log Management
- Digital Forensics

---

# Examples of SIEM Platforms

Several commercial and open-source SIEM solutions are widely used, including:

- Wazuh
- Splunk Enterprise Security
- Microsoft Sentinel
- IBM QRadar
- Google Security Operations (Chronicle)
- LogRhythm
- Elastic Security

Although each platform has different capabilities, they all aim to centralize security monitoring and improve threat detection.

---

# How This Relates to Wazuh

Wazuh is an open-source platform that provides SIEM capabilities by collecting, storing, analyzing, and correlating security events from across an organization's infrastructure.

Within Wazuh:

| Wazuh Component | SIEM Function |
|-----------------|---------------|
| **Agent** | Collects logs and security events from monitored endpoints. |
| **Manager** | Analyzes incoming events using decoders and detection rules, correlates events, and generates alerts. |
| **Indexer** | Stores and indexes alerts and security events for fast searching and historical analysis. |
| **Dashboard** | Provides a centralized interface where analysts can search logs, investigate alerts, monitor agents, and visualize security events. |

In addition to traditional SIEM functionality, Wazuh also provides several **Extended Detection and Response (XDR)** capabilities, including:

- File Integrity Monitoring (FIM)
- Vulnerability Detection
- Security Configuration Assessment (SCA)
- Rootcheck
- Active Response
- Endpoint Inventory

These additional features allow Wazuh to move beyond traditional log management and provide a more comprehensive security monitoring platform.

---

# Key Takeaways

- SIEM stands for **Security Information and Event Management**.
- A SIEM centralizes security logs from multiple systems into a single platform.
- SIEM platforms collect, normalize, store, correlate, and analyze security events.
- Event correlation enables the detection of complex attacks that individual logs may not reveal.
- Wazuh implements SIEM capabilities through its Agent, Manager, Indexer, and Dashboard while also providing XDR features for advanced threat detection and response.

---

# References

- Wazuh Documentation: https://documentation.wazuh.com/
- NIST Computer Security Resource Center: https://csrc.nist.gov/
