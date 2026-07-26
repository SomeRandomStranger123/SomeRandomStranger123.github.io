---
title: "Writeups"
---

# 🧠 Writeups

A categorized index of all my writeups across cloud security, AWS, CTFs, and tooling.

Legend:  
✅ = Complete & Published  
📝 = In Progress  
🔒 = Not Started  

---

## 📋 Contents

- [🔐 Blue Team Activities](#-blue-team-activities)  
- [🔐 Red Team Activities](#-red-team-activities)  
- [🏴‍☠️ CTF Writeups](#-ctf-writeups)  
- [🧪 Tools & Techniques](#-tools--techniques)  
- [🗂️ Miscellaneous](#-miscellaneous)  

---

## 🔐 Blue Team Activities

### 🧪 Pwned Labs  
- 🔒 **[Initial Access](writeups/pwnedlabs_breach_in_the_cloud)** – Utilizing PowerShell or Grep to analyze CloudTrail logs, identify suspicious AWS activity, trace attacker steps, and confirm breaches.  
  _Tags: #AWS #CloudTrail #Forensics #IncidentResponse_  
  _Last Updated: June 2025_  

### 🔍 Cybr Labs  
- 🔒 *(Coming soon)*

---

## 🔐 Red Team Activities

### 🛠️ CloudGoat (AWS PenTesting) Scenarios — Listed from Hard → Easy  

#### 🔴 Hard  
- 📝 **[Secrets in the Cloud](writeups/cloudgoat_secrets_in_the_cloud)** – Discover and exploit exposed secrets in an AWS environment.  
  _Tags: #AWS #Secrets #PrivilegeEscalation_  
  _Last Updated: June 2025_  

#### 🟡 Medium  
- ✅ **[Vulnerable Cognito](writeups/cloudgoat_vulnerable_cognito)** – Exploit a Cognito misconfiguration or vulnerability.  
  _Tags: #AWS #Cognito #Authentication_  
  _Last Updated: June 2025_  

#### 🟢 Easy  
- ✅ **[Beanstalk Secrets](writeups/cloudgoat_beanstalk_secrets)** – Leverage secrets exposed via AWS Elastic Beanstalk configs.  
  _Tags: #AWS #Beanstalk #Secrets_  
  _Last Updated: June 2025_  
- ✅ **[SNS Secrets](writeups/cloudgoat_sns_secrets)** – Secrets leaked through SNS topics and subscriptions.  
  _Tags: #AWS #SNS #Secrets_  
  _Last Updated: June 2025_  
- ✅ **[Lambda Privilege Escalation](writeups/cloudgoat_lambda_privesc)** – Exploit Lambda permissions for privilege escalation.  
  _Tags: #AWS #Lambda #PrivilegeEscalation_  
  _Last Updated: June 2025_  
- ✅ **[IAM Privesc by Rollback](writeups/cloudgoat_iam_privesc_by_rollback)** – Use `iam:SetDefaultPolicyVersion` to escalate privileges.  
  _Tags: #AWS #IAM #PrivilegeEscalation_  
  _Last Updated: June 2025_  

---

### Leftover CloudGoat — Planned for Completion  

- 🔒 **IAM Privesc by Key Rotation** – Abuse old access keys after rotation.  
- 🔒 **SQS Flag Shop** – SQS misconfigurations & flag retrieval.  
- 🔒 **Vulnerable Lambda** – Lambda function vulnerability exploration.  
- 🔒 **Cloud Breach S3** – S3 bucket exposure attack chain.  
- 🔒 **IAM Privesc by Attachment** – Privilege escalation via policy attachment.  
- 🔒 **EC2 SSRF** – SSRF from EC2 to internal endpoints.  
- 🔒 **ECS Takeover** – ECS misconfiguration or credential takeover.  
- 🔒 **RDS Snapshot** – Access via publicly shared RDS snapshots.  
- 🔒 **Glue Privesc** – Glue job-based privilege escalation.  
- 🔒 **RCE Web App** – Remote code execution via web app.  
- 🔒 **CodeBuild Secrets** – Secret leakage through CodeBuild.  
- 🔒 **Detection Evasion** – Techniques to evade CloudTrail or monitoring.  
- 🔒 **ECS EFS Attack** – ECS compromise via insecurely mounted EFS volumes.  

---

## 🏴‍☠️ CTF Writeups

- _(Coming soon)_  

---

## 🧪 Tools & Techniques

- _(Coming soon)_  

---

## 🗂️ Miscellaneous

- _(Coming soon)_

---

*This index is continuously updated. Feel free to open an issue or PR on [GitHub](https://github.com/SomeRandomStranger123) to contribute or request features!*
