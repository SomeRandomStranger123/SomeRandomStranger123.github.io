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

### 🧪 Pwnd Labs  
- 🔒 **[Initial Access](pwnedlabs_breach_in_the_cloud)** – Utilizing PowerShell or Grep to analyze CloudTrail logs, identify suspicious AWS activity, trace attacker steps, and confirm breaches.  
  _Tags: #AWS #CloudTrail #Forensics #IncidentResponse_  
  _Last Updated: June 2025_  

### 🔍 Cybr Labs  
- 🔒 *(Coming soon)*

---

## 🔐 Red Team Activities

### 🛠️ CloudGoat (AWS PenTesting) Scenarios — Listed from Hard → Easy  

#### 🔴 Hard  
- 📝 **[Secrets in the Cloud](/cloudgoat_secrets_in_the_cloud.md)** – Discover and exploit exposed secrets in an AWS environment.  
  _Tags: #AWS #Secrets #PrivilegeEscalation_  
  _Last Updated: June 2025_  

#### 🟡 Medium  
- ✅ **[Vulnerable Cognito](cloudgoat_vulnerable_cognito.md)** – Exploit a Cognito misconfiguration or vulnerability.  
  _Tags: #AWS #Cognito #Authentication_  
  _Last Updated: June 2025_  

#### 🟢 Easy  
- ✅ **[Beanstalk Secrets](/cloudgoat_beanstalk_secrets.md)** – Leverage secrets exposed via AWS Elastic Beanstalk configs.  
  _Tags: #AWS #Beanstalk #Secrets_  
  _Last Updated: June 2025_  
- ✅ **[SNS Secrets](/cloudgoat_sns_secrets.md)** – Secrets leaked through SNS topics and subscriptions.  
  _Tags: #AWS #SNS #Secrets_  
  _Last Updated: June 2025_  
- ✅ **[Lambda Privilege Escalation](/cloudgoat_lambda_privesc.md)** – Exploit Lambda permissions for privilege escalation.  
  _Tags: #AWS #Lambda #PrivilegeEscalation_
  _Last Updated: June 2025_  
- ✅ **[IAM Privesc by Rollback](/cloudgoat_iam_privesc_by_rollback.md)** – Use `iam:SetDefaultPolicyVersion` to escalate privileges.  
  _Tags: #AWS #IAM #PrivilegeEscalation_  
  _Last Updated:  June 2025_  
---

### Leftover CloudGoat — Planned for Completion  

- 🔒 **[IAM Privesc by Key Rotation](/cloudgoat_iam_privesc_by_key_rotation.md)** – Abuse old access keys after rotation.  
- 🔒 **[SQS Flag Shop](/cloudgoat_sqs_flag_shop.md)** – SQS misconfigurations & flag retrieval.  
- 🔒 **[Vulnerable Lambda](cloudgoat/cloudgoat_vulnerable_lambda.md)** – Lambda function vulnerability exploration.  
- 🔒 **[Cloud Breach S3](cloudgoat/cloudgoat_cloud_breach_s3.md)** – S3 bucket exposure attack chain.  
- 🔒 **[IAM Privesc by Attachment](cloudgoat/cloudgoat_iam_privesc_by_attachment.md)** – Privilege escalation via policy attachment.  
- 🔒 **[EC2 SSRF](cloudgoat/cloudgoat_ec2_ssrf.md)** – SSRF from EC2 to internal endpoints.  
- 🔒 **[ECS Takeover](cloudgoat/cloudgoat_ecs_takeover.md)** – ECS misconfiguration or credential takeover.  
- 🔒 **[RDS Snapshot](cloudgoat/cloudgoat_rds_snapshot.md)** – Access via publicly shared RDS snapshots.  
- 🔒 **[Glue Privesc](cloudgoat/cloudgoat_glue_privesc.md)** – Glue job-based privilege escalation.  
- 🔒 **[RCE Web App](cloudgoat/cloudgoat_rce_web_app.md)** – Remote code execution via web app.  
- 🔒 **[CodeBuild Secrets](cloudgoat/cloudgoat_codebuild_secrets.md)** – Secret leakage through CodeBuild.  
- 🔒 **[Detection Evasion](cloudgoat/cloudgoat_detection_evasion.md)** – Techniques to evade CloudTrail or monitoring.  
- 🔒 **[ECS EFS Attack](cloudgoat/cloudgoat_ecs_efs_attack.md)** – ECS compromise via insecurely mounted EFS volumes.  

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

