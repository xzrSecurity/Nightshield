# NightShield

> **Detect. Secure. Document.**
>
> Open-source cloud security monitoring lab built to turn raw telemetry into actionable detection, visibility, and incident analysis.

---

## Overview

**NightShield** is a cloud security monitoring project designed to detect suspicious activity, surface insecure configurations, and document investigations inside a reproducible lab environment. It combines centralized telemetry, runtime detection, and cloud posture assessment to simulate a compact but realistic defensive monitoring stack.[web:19][web:23][web:21][web:63]

The project is built around open-source tooling and an engineering-first workflow: deploy the lab, generate telemetry, trigger controlled detection scenarios, analyze alerts, and document each finding like a real analyst case. Wazuh provides SIEM and XDR-style visibility across endpoints and cloud workloads, Falco covers runtime detection, and Prowler adds posture assessment across major cloud environments.[web:19][web:64][web:21][web:66]

---

## Mission

NightShield exists to answer a simple question: **can a small cloud lab detect both bad configuration and suspicious runtime behavior using only open-source tools?** The project is structured to demonstrate not just tool installation, but a full monitoring chain from data collection to alert triage and technical reporting.[web:23][web:21][web:63]

This repository is also built as a portfolio project for cloud security, SOC, and detection engineering growth. The emphasis is on reproducibility, clarity, and investigation quality rather than on building a large but shallow lab.[cite:5][cite:4][cite:33]

---

## Core Stack

| Layer | Tool | Purpose |
|---|---|---|
| SIEM / XDR | **Wazuh** | Centralized log collection, monitoring, threat detection, and security event analysis across endpoints and cloud workloads.[web:19][web:23][web:64] |
| Runtime Security | **Falco** | Real-time detection of abnormal behavior on Linux hosts, containers, Kubernetes, and cloud-connected environments using rules over kernel/runtime events.[web:15][web:21][web:65] |
| Cloud Posture | **Prowler** | Open-source cloud security assessment for AWS, Azure, and GCP, with checks for auditing, hardening, and continuous monitoring.[web:63][web:66][web:68] |
| Infrastructure | **Terraform** | Reproducible lab provisioning and infrastructure-as-code workflow. |
| Cloud Provider | **AWS** | Primary lab target for cloud logging, workload hosting, and security testing. |
| Workload | **Ubuntu Linux VM** | Endpoint telemetry, runtime activity, and controlled attack simulation. |

---

## What NightShield Monitors

NightShield is designed to observe both **cloud control-plane activity** and **runtime behavior**. That includes cloud logs, host events, process activity, suspicious shell execution, configuration drift, and posture findings that indicate insecure exposure or weak hardening.[web:23][web:21][web:63]

The intended visibility model is layered:

- **Wazuh** for aggregation, alerting, and correlation across the lab.[web:19][web:23]
- **Falco** for runtime signals such as suspicious execution, sensitive file access, or unexpected system behavior.[web:21][web:65]
- **Prowler** for posture review, misconfiguration discovery, and security baseline validation.[web:63][web:66]

---

## Detection Themes

The lab focuses on realistic defensive use cases instead of generic demo alerts. Initial scenarios include:

- Suspicious shell activity on monitored Linux systems.
- Access to sensitive files or abnormal runtime behavior.
- Risky cloud configuration changes.
- Overly permissive security groups or exposed services.
- Cloud posture weaknesses discovered during assessment scans.
- Unusual outbound behavior or execution patterns requiring triage.[web:21][web:65][web:63]

Each scenario is intended to be documented with setup steps, commands, telemetry evidence, triggered alerts, analyst interpretation, impact assessment, and remediation notes. This project treats documentation as part of detection engineering rather than as an afterthought.[cite:4][cite:34]

---

## Architecture Direction

The first version of NightShield is intentionally compact: one AWS lab, one Linux workload, one centralized monitoring layer, and a controlled set of detection scenarios. Wazuh can protect cloud and containerized workloads, Falco can forward alert events for downstream analysis, and Prowler can be run from a workstation or cloud-based environment to assess the target account.[web:25][web:21][web:63]

This small footprint keeps the project realistic to build while still demonstrating core security monitoring concepts: telemetry collection, runtime detection, posture review, investigation workflow, and technical reporting.[web:23][web:21][cite:5]

```text
                    +----------------------+
                    |       AWS Lab        |
                    |  CloudTrail / VPC    |
                    |      Flow Logs       |
                    +----------+-----------+
                               |
                               v
+-------------+      +-------------------+      +----------------+
|  Prowler    |----->|     NightShield   |<-----|   Falco Agent  |
| CSPM Audit  |      |   Wazuh Platform  |      | Runtime Events |
+-------------+      | SIEM / Correlation|      +----------------+
                     +---------+---------+
                               ^
                               |
                        +------+------+
                        | Ubuntu Host |
                        | Wazuh Agent |
                        +-------------+
```

---

## Repository Structure

```text
NightShield/
├── README.md
├── LICENSE
├── .gitignore
├── SECURITY.md
├── docs/
│   ├── architecture.md
│   ├── deployment.md
│   ├── detections.md
│   ├── scenarios.md
│   └── roadmap.md
├── incidents/
│   └── README.md
├── screenshots/
│   └── .gitkeep
├── terraform/
│   └── README.md
├── wazuh/
│   └── README.md
├── falco/
│   └── README.md
└── prowler/
    └── README.md
```

This layout separates infrastructure, detection content, evidence, and investigation notes so the repo stays readable as the lab grows. It also makes the project easier to review for recruiters or technical readers who want to jump directly to architecture, detections, or incident write-ups.[web:42][web:45][cite:34]

---

## Build Philosophy

NightShield is not meant to be a random collection of security tools. The goal is to build a coherent open-source monitoring pipeline where every component has a clear role and every alert can be explained, reproduced, and improved.[web:19][web:21][web:66]

That means the project prioritizes:

- Reproducible deployment.
- Clean separation between logging, detection, and posture assessment.
- Analyst-style investigation notes with evidence.
- Controlled attack simulation instead of noisy lab chaos.
- Continuous refinement of rules, documentation, and remediation paths.[cite:4][cite:33][cite:34]

---

## Roadmap

### Phase 1
- Create the repository structure.
- Define the AWS lab architecture.
- Deploy the first Ubuntu workload.
- Install Wazuh and connect the endpoint.

### Phase 2
- Deploy and tune Falco on the monitored host.[web:21][web:65]
- Enable key cloud telemetry sources.
- Run initial Prowler assessments and baseline the environment.[web:63][web:66]

### Phase 3
- Execute controlled detection scenarios.
- Capture alerts, screenshots, and logs.
- Write incident case files and remediation notes.[cite:4][cite:34]

### Phase 4
- Expand detections.
- Improve rule quality and reduce noise.
- Consider containers or Kubernetes for a more advanced runtime layer.[web:15][web:21]

---

## Why This Project Matters

Wazuh is positioned as an open-source platform for threat detection, incident response, SIEM, and XDR-style monitoring across endpoints and cloud workloads, while Falco specializes in real-time runtime detection and Prowler adds large-scale cloud security assessment coverage.[web:19][web:64][web:21][web:66] Together, they form a strong open-source foundation for a cloud monitoring lab that demonstrates both blue-team fundamentals and practical detection engineering concepts.[web:23][web:65][web:63]

NightShield is therefore designed as more than a homelab. It is a documented security project focused on visibility, analysis quality, and defensive reasoning under realistic constraints.[cite:5][cite:2][cite:3]

---

## Status

**Current phase:** repository design and documentation foundation.[cite:5]

Planned next step: define the architecture and deploy the first AWS-based monitoring components.[cite:5]

---

## License

This project is intended to be released under the MIT License.
