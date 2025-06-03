# 🧠 Pentesting Writeups

A categorized index of all my writeups across cloud security, AWS, CTFs, and tooling.

Legend:  
✅ = Complete & Published  
📝 = In Progress  
🕳️ = Not Started  

---

## 🛠️ CloudGoat Scenarios

### 🟢 Easy  
- ✅ [beanstalk_secrets](cloudgoat/cloudgoat_beanstalk_secrets.md) – Leverages secrets exposed via AWS Elastic Beanstalk configuration files.  
- ✅ [sns_secrets](cloudgoat/cloudgoat_sns_secrets.md) – Involves secrets leaked through SNS topics and subscriptions.  
- ✅ [lambda_privesc](cloudgoat/cloudgoat_lambda_privesc.md) – Exploits Lambda permissions for privilege escalation.  
- 🕳️ [iam_privesc_by_key_rotation](cloudgoat/cloudgoat_iam_privesc_by_key_rotation.md) – Explores abusing old access keys after key rotation *(link added; scenario may not be documented yet)*.  
- ✅ [iam_privesc_by_rollback](cloudgoat/cloudgoat_iam_rollback_attack.md) – Demonstrates privilege escalation using `iam:SetDefaultPolicyVersion`.  
- 🕳️ [sqs_flag_shop](cloudgoat/cloudgoat_sqs_flag_shop.md) – Scenario involving SQS misconfigurations and flag retrieval *(placeholder link)*.  

---

### 🟡 Medium  
- 🕳️ [vulnerable_cognito](cloudgoat/cloudgoat_vulnerable_cognito.md) – Cognito misconfiguration or vulnerability scenario *(placeholder)*.  
- 🕳️ [vulnerable_lambda](cloudgoat/cloudgoat_vulnerable_lambda.md) – Lambda function vulnerability exploration *(placeholder)*.  
- 🕳️ [cloud_breach_s3](cloudgoat/cloudgoat_cloud_breach_s3.md) – S3 bucket exposure or attack chain scenario *(placeholder)*.  
- 🕳️ [iam_privesc_by_attachment](cloudgoat/cloudgoat_iam_privesc_by_attachment.md) – IAM privilege escalation via policy attachment *(placeholder)*.  
- 🕳️ [ec2_ssrf](cloudgoat/cloudgoat_ec2_ssrf.md) – SSRF from EC2 to access metadata/internal endpoints *(placeholder)*.  
- 🕳️ [ecs_takeover](cloudgoat/cloudgoat_ecs_takeover.md) – ECS misconfiguration or credential takeover *(placeholder)*.  
- 🕳️ [rds_snapshot](cloudgoat/cloudgoat_rds_snapshot.md) – Access via publicly shared RDS snapshots *(placeholder)*.  
- 🕳️ [glue_privesc](cloudgoat/cloudgoat_glue_privesc.md) – Glue job-based privilege escalation *(placeholder)*.  

---

### 🔴 Hard  
- 📝 [secrets_in_the_cloud](cloudgoat/secrets_in_the_cloud.md) – Focuses on discovering and exploiting exposed secrets in an AWS environment.  
- 🕳️ [rce_web_app](cloudgoat/cloudgoat_rce_web_app.md) – Remote Code Execution via vulnerable web app *(placeholder)*.  
- 🕳️ [codebuild_secrets](cloudgoat/cloudgoat_codebuild_secrets.md) – Secret leakage through CodeBuild environments or artifacts *(placeholder)*.  
- 🕳️ [detection_evasion](cloudgoat/cloudgoat_detection_evasion.md) – Techniques for evading CloudTrail or other monitoring *(placeholder)*.  
- 🕳️ [ecs_efs_attack](cloudgoat/cloudgoat_ecs_efs_attack.md) – ECS compromise via insecurely mounted EFS volumes *(placeholder)*.  
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
