AWS GuardDuty Threat Detection Lab
Domain: Cloud Security | Threat Detection | Incident Investigation
Tools: Amazon GuardDuty · AWS CloudTrail · AWS S3 · AWS Console
Date Completed: April 28, 2026

Project Overview
This project demonstrates cloud threat detection and incident investigation using Amazon GuardDuty and AWS CloudTrail in a personal AWS lab environment. The goal was to simulate realistic cloud attack scenarios, investigate findings the way a SOC analyst would, and produce a formal incident report as a portfolio deliverable.
GuardDuty was enabled on a personal AWS account, CloudTrail was configured to capture a full management event audit trail, and sample findings were generated to simulate two distinct threat scenarios. Each finding was investigated by examining GuardDuty finding details, cross-referencing CloudTrail event history, and documenting analyst conclusions and recommended response actions.

What Was Investigated
Finding 1 — Credential Exfiltration (High Severity)
Type: UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration.OutsideAWS
EC2 instance credentials were detected being used from an external IP address outside the instance — a strong indicator that temporary AWS credentials were stolen and are being leveraged by a threat actor from outside AWS infrastructure. This finding maps to MITRE ATT&CK technique T1552.005 — Cloud Instance Metadata API.
Investigation included analyzing the actor IP address, identifying the affected resource, cross-referencing CloudTrail for corroborating API call evidence, and documenting a full incident response playbook.

Finding 2 — EC2 Instance Group Compromise (Critical Severity)
Type: AttackSequence:EC2/CompromisedInstanceGroup
GuardDuty's machine learning correlation engine detected three signals across nine EC2 instances in an Auto Scaling Group, identifying them as a coordinated multi-stage attack chain. This is GuardDuty's most advanced detection capability — correlating separate events across time and resources rather than flagging individual anomalies.
The three-signal attack chain mapped to the following MITRE ATT&CK tactics:
SignalTacticObserved Behavior1Command & ControlInstance queried a blackholed C2 domain2ExfiltrationInstance queried a Drop Point data collection domain3ImpactInstance communicating with a known abused domain

Skills Demonstrated

Enabling and configuring Amazon GuardDuty for continuous cloud threat monitoring
Configuring AWS CloudTrail for management event audit logging
Reading and triaging GuardDuty findings by severity and finding type
Cross-referencing GuardDuty findings against CloudTrail event history
Identifying and documenting false positives with supporting context
MITRE ATT&CK tactic mapping for cloud-based attack techniques
Formal incident report writing for both technical and executive audiences


Tools Used
ToolPurposeAmazon GuardDutyContinuous threat detection — ingests VPC Flow Logs, CloudTrail, DNS logsAWS CloudTrailManagement event audit trail — raw API call loggingAWS S3CloudTrail log storageAWS ConsoleLab configuration, finding investigation, event history analysis

Repository Structure
aws-guardduty-threat-detection/
│
├── README.md                                        ← This file
├── Bryan_Sykes_AWS_GuardDuty_Incident_Report.docx  ← Full incident report
│
└── screenshots/
    ├── 01-guardduty-enabled-summary.png
    ├── 02-cloudtrail-trail-active.png
    ├── 03-guardduty-sample-findings-list.png
    ├── 04-guardduty-finding-credential-exfiltration.png
    ├── 05-cloudtrail-event-history.png
    ├── 06-cloudtrail-createsamplefindings-json.png
    ├── 07-guardduty-critical-ec2-compromised-instancegroup.png
    ├── 08-guardduty-autoscaling-resources.png
    └── 09-guardduty-attack-signals-timeline.png

Key Takeaways
GuardDuty operates as an agentless detection service — no software is installed on monitored instances. It detects. CloudTrail explains. Together they form the foundation of cloud incident investigation in AWS environments.
The AttackSequence finding type demonstrated how ML-based correlation across multiple signals can identify sophisticated, multi-stage attacks that individual signature-based rules would miss entirely — a capability increasingly relevant as threat actors adopt more advanced cloud-native attack techniques.
False positive triage is as important as detection. A Low severity finding triggered by legitimate administrative activity (CloudTrail trail creation) was correctly identified and closed with CloudTrail context — demonstrating that alert investigation requires environmental awareness, not just tool output.

Notes

All findings were generated using GuardDuty's built-in sample findings generator in a personal sandbox account
No live infrastructure was attacked or compromised
AWS account ID has been masked in all documentation for public repository safety
GuardDuty was disabled after the lab to avoid post-trial charges


Part of an ongoing cybersecurity portfolio. Additional projects cover Security Onion SIEM detection, Kali Linux attack simulation, GRC framework assessments, and application security vulnerability analysis.
