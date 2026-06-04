NightShield
<p align="center">
<img src="https://img.shields.io/badge/Open%20Source-Yes-00c853?style=for-the-badge&logo=opensourceinitiative&logoColor=white" alt="Open Source">
<img src="https://img.shields.io/badge/AWS-Lab-232F3E?style=for-the-badge&logo=amazonwebservices&logoColor=white" alt="AWS Lab">
<img src="https://img.shields.io/badge/Wazuh-SIEM%20%2F%20XDR-0052CC?style=for-the-badge&logo=wazuh&logoColor=white" alt="Wazuh">
<img src="https://img.shields.io/badge/Falco-Runtime%20Security-00AEC7?style=for-the-badge&logo=falco&logoColor=white" alt="Falco">
<img src="https://img.shields.io/badge/Prowler-Cloud%20Posture-7B61FF?style=for-the-badge&logo=prowlarr&logoColor=white" alt="Prowler">
<img src="https://img.shields.io/badge/Terraform-IaC-844FBA?style=for-the-badge&logo=terraform&logoColor=white" alt="Terraform">
<img src="https://img.shields.io/badge/Ubuntu-Workload-E95420?style=for-the-badge&logo=ubuntu&logoColor=white" alt="Ubuntu">
<img src="https://img.shields.io/badge/Status-Building-111111?style=for-the-badge&logo=github&logoColor=white" alt="Status">
</p>

<p align="center">
<strong>Detect. Secure. Document.</strong>
</p>

<p align="center">
Open-source cloud security monitoring lab designed to transform telemetry into detection, visibility, and incident analysis.
</p>

Overview
NightShield is a cloud security monitoring project built around a realistic, reproducible lab environment. Its purpose is to detect suspicious activity, expose insecure cloud configurations, and document technical investigations with the same discipline used in real defensive operations.

The project combines three complementary layers: centralized monitoring with Wazuh, runtime detection with Falco, and cloud posture assessment with Prowler. Wazuh is positioned as an open-source SIEM/XDR platform for endpoints and cloud workloads, Falco focuses on runtime security across Linux, containers, Kubernetes, and cloud environments, and Prowler provides open-source cloud security assessment across AWS, Azure, and GCP.

Mission
NightShield is built to answer a practical blue-team question: can a small open-source cloud lab provide useful visibility across configuration risk, system activity, and suspicious runtime behavior? The goal is not to pile tools together, but to create a coherent monitoring pipeline where events can be collected, understood, investigated, and improved over time.

This repository is also designed as a portfolio project focused on cloud security monitoring, SOC operations, and detection engineering progression. The documentation emphasizes commands, evidence, screenshots, analyst reasoning, and remediation paths rather than generic summaries.

Core Stack
Layer	Tool	Role
Monitoring / SIEM	Wazuh	Collects and analyzes event data from endpoints, network devices, cloud workloads, and applications for broader security visibility.
Runtime Detection	Falco	Detects abnormal behavior in real time across Linux systems, containers, Kubernetes, and cloud-connected workloads.
Cloud Posture	Prowler	Assesses cloud environments for security gaps, hardening issues, and audit findings across major platforms.
Infrastructure as Code	Terraform	Keeps lab deployment reproducible and easier to document.
Cloud Platform	AWS	Primary lab target for first deployment and cloud telemetry collection.
Monitored Workload	Ubuntu Linux VM	Host used for telemetry, tests, runtime detections, and controlled attack simulations.
Monitoring Scope
NightShield focuses on both cloud-level visibility and runtime-level visibility. That includes cloud audit signals, workload telemetry, suspicious process execution, risky security changes, and posture findings that can explain why the environment is exposed in the first place.

The monitoring model is intentionally layered:

Wazuh centralizes telemetry and security alerting across the lab.

Falco provides runtime context for suspicious activity on the host or future container layer.

Prowler measures the security posture of the cloud environment and highlights hardening gaps.

Detection Goals
The first versions of NightShield are built around realistic detection and analysis scenarios rather than artificial demo content. Planned scenarios include:

Suspicious shell execution on Linux.

Sensitive file access.

Risky cloud configuration changes.

Overly permissive security groups.

Unexpected outbound activity.

Posture weaknesses identified during cloud assessment scans.

Each scenario is intended to be documented as a mini incident case with setup context, commands used, telemetry collected, triggered alerts, analyst interpretation, risk assessment, and remediation guidance. This makes documentation part of the technical value of the project instead of a separate afterthought.

Architecture Direction
NightShield starts with a compact architecture: one AWS lab, one monitored Ubuntu host, one central visibility layer, and a controlled set of attack simulations. This keeps the scope realistic while still demonstrating telemetry collection, runtime monitoring, posture assessment, and documentation workflows.

text
                    +----------------------+
                    |       AWS Lab        |
                    |  Audit & Flow Logs   |
                    +----------+-----------+
                               |
                               v
+-------------+      +-------------------+      +----------------+
|  Prowler    |----->|    NightShield    |<-----|   Falco Agent  |
| CSPM Audit  |      |   Wazuh Platform  |      | Runtime Events |
+-------------+      | SIEM / Correlation|      +----------------+
                     +---------+---------+
                               ^
                               |
                        +------+------+
                        | Ubuntu Host |
                        | Wazuh Agent |
                        +-------------+
Repository Structure
text
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
A structured README should explain what the project does, how it is used, and how the repository is organized, and this layout supports that by separating infrastructure, tooling, detections, and evidence clearly for readers and recruiters.

Project Philosophy
NightShield is built with an engineering mindset rather than a screenshot-only mindset. Every component should have a defined role, every detection should be testable, and every alert should be explainable in terms of source, impact, and remediation.

The project therefore prioritizes:

Reproducible deployment.

Open-source visibility and detection tooling.

Clean documentation with commands and screenshots.

Incident-style technical notes.

A gradual roadmap from simple lab to more advanced monitoring scenarios.

Roadmap
Phase 1
Create the repository and documentation foundation.

Define the AWS lab architecture.

Prepare Terraform for the first workload.

Set up the initial monitoring plan.

Phase 2
Deploy the first Ubuntu instance.

Install Wazuh and validate telemetry ingestion.

Install Falco and test baseline runtime detections.

Run initial Prowler scans for posture visibility.

Phase 3
Simulate controlled attack scenarios.

Capture alerts, logs, and screenshots.

Write incident notes and remediation recommendations.

Phase 4
Expand detection coverage.

Tune rules and reduce noise.

Add more advanced workloads such as containers or Kubernetes when the first version is stable.

Status
Current phase: repository creation and documentation setup.

Next step: finalize the repository structure, add core policy files, and begin architecture documentation.

License
This project is intended to be released under the MIT License.
