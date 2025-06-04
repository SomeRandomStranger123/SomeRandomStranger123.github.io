# 🧠 Pentesting Writeups

A categorized index of all my writeups across cloud security, AWS, CTFs, and tooling.

Legend:  
✅ = Complete & Published  
📝 = In Progress  
🔒 = Not Started  

---

## 🛠️ CloudGoat Scenarios

### 🟢 Easy  
- ✅ [beanstalk_secrets](/cloudgoat_beanstalk_secrets.md) – Leverages secrets exposed via AWS Elastic Beanstalk configuration files.  
- ✅ [sns_secrets](/cloudgoat_sns_secrets.md) – Involves secrets leaked through SNS topics and subscriptions.  
- ✅ [lambda_privesc](/cloudgoat_lambda_privesc.md) – Exploits Lambda permissions for privilege escalation.  
- 🔒 [iam_privesc_by_key_rotation](/cloudgoat_iam_privesc_by_key_rotation.md) – Explores abusing old access keys after key rotation *(not yet documented)*.  
- ✅ [iam_privesc_by_rollback](/cloudgoat_iam_privesc_by_rollback.md) – Demonstrates privilege escalation using `iam:SetDefaultPolicyVersion`.  
- 🔒 [sqs_flag_shop](/cloudgoat_sqs_flag_shop.md) – Scenario involving SQS misconfigurations and flag retrieval *(not yet documented)*.  

---

### 🟡 Medium  
- 🔒 [vulnerable_cognito](cloudgoat/cloudgoat_vulnerable_cognito.md) – Cognito misconfiguration or vulnerability scenario *(not yet documented)*.  
- 🔒 [vulnerable_lambda](cloudgoat/cloudgoat_vulnerable_lambda.md) – Lambda function vulnerability exploration *(not yet documented)*.  
- 🔒 [cloud_breach_s3](cloudgoat/cloudgoat_cloud_breach_s3.md) – S3 bucket exposure or attack chain scenario *(not yet documented)*.  
- 🔒 [iam_privesc_by_attachment](cloudgoat/cloudgoat_iam_privesc_by_attachment.md) – IAM privilege escalation via policy attachment *(not yet documented)*.  
- 🔒 [ec2_ssrf](cloudgoat/cloudgoat_ec2_ssrf.md) – SSRF from EC2 to access metadata/internal endpoints *(not yet documented)*.  
- 🔒 [ecs_takeover](cloudgoat/cloudgoat_ecs_takeover.md) – ECS misconfiguration or credential takeover *(not yet documented)*.  
- 🔒 [rds_snapshot](cloudgoat/cloudgoat_rds_snapshot.md) – Access via publicly shared RDS snapshots *(not yet documented)*.  
- 🔒 [glue_privesc](cloudgoat/cloudgoat_glue_privesc.md) – Glue job-based privilege escalation *(not yet documented)*.  

---

### 🔴 Hard  
- 📝 [secrets_in_the_cloud](/secrets_in_the_cloud.md) – Focuses on discovering and exploiting exposed secrets in an AWS environment.  
- 🔒 [rce_web_app](cloudgoat/cloudgoat_rce_web_app.md) – Remote Code Execution via vulnerable web app *(not yet documented)*.  
- 🔒 [codebuild_secrets](cloudgoat/cloudgoat_codebuild_secrets.md) – Secret leakage through CodeBuild environments or artifacts *(not yet documented)*.  
- 🔒 [detection_evasion](cloudgoat/cloudgoat_detection_evasion.md) – Techniques for evading CloudTrail or other monitoring *(not yet documented)*.  
- 🔒 [ecs_efs_attack](cloudgoat/cloudgoat_ecs_efs_attack.md) – ECS compromise via insecurely mounted EFS volumes *(not yet documented)*.  
---

## ☁️ AWS Pentesting (General)

_(Coming soon)_

---

## 🏴‍☠️ CTF Writeups

_(Coming soon)_

---

## 🧪 Tools & Techniques

_(Coming soon)_

---

## 🗂️ Miscellaneous

_(Coming soon)_
