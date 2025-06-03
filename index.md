# 🧠 Pentesting Writeups

A categorized index of all my writeups across cloud security, AWS, CTFs, and tooling.

Legend:  
✅ = Complete & Published  
📝 = In Progress  
🕳️ = Not Started  

---

## 🛠️ CloudGoat Scenarios

### 🟢 Easy  
✅ [beanstalk_secrets](cloudgoat/cloudgoat_beanstalk_secrets.md) – Leverages secrets exposed via AWS Elastic Beanstalk configuration files.
✅ [sns_secrets](cloudgoat/cloudgoat_sns_secrets.md) – Involves secrets leaked through SNS topics and subscriptions.
✅ [lambda_privesc](cloudgoat/cloudgoat_lambda_privesc.md) – Exploits Lambda permissions for privilege escalation.
🕳️ [iam_privesc_by_key_rotation](cloudgoat/cloudgoat_iam_privesc_by_key_rotation.md) – Explores abusing old access keys after key rotation (link added but scenario may not be documented yet).
✅ [iam_privesc_by_rollback](cloudgoat/cloudgoat_iam_rollback_attack.md) – Demonstrates privilege escalation using `iam:SetDefaultPolicyVersion`.
🕳️ [sqs_flag_shop](cloudgoat/cloudgoat_sqs_flag_shop.md) – Scenario involving SQS misconfigurations and flag retrieval (placeholder link).


---

### 🟡 Medium 
🕳️ [vulnerable_cognito](cloudgoat/cloudgoat_vulnerable_cognito.md) – Placeholder for Cognito misconfiguration or vulnerability scenario.
🕳️ [vulnerable_lambda](cloudgoat/cloudgoat_vulnerable_lambda.md) – Placeholder for Lambda function vulnerability exploration.
🕳️ [cloud_breach_s3](cloudgoat/cloudgoat_cloud_breach_s3.md) – S3 bucket exposure or attack chain scenario.
🕳️ [iam_privesc_by_attachment](cloudgoat/cloudgoat_iam_privesc_by_attachment.md) – Placeholder for IAM privilege escalation via policy attachment.
🕳️ [ec2_ssrf](cloudgoat/cloudgoat_ec2_ssrf.md) – Exploiting SSRF from EC2 to access metadata services or internal endpoints.
🕳️ [ecs_takeover](cloudgoat/cloudgoat_ecs_takeover.md) – Placeholder for ECS misconfiguration or credential takeover scenario.
🕳️ [rds_snapshot](cloudgoat/cloudgoat_rds_snapshot.md) – Gaining access via publicly shared RDS snapshots.
🕳️ [glue_privesc](cloudgoat/cloudgoat_glue_privesc.md) – Placeholder for Glue job-based privilege escalation. 

---

### 🔴 Hard  
📝 [secrets_in_the_cloud](cloudgoat/secrets_in_the_cloud.md) – Focuses on discovering and exploiting exposed secrets in an AWS environment.
🕳️ [rce_web_app](cloudgoat/cloudgoat_rce_web_app.md) – Remote Code Execution via vulnerable web app.
🕳️ [codebuild_secrets](cloudgoat/cloudgoat_codebuild_secrets.md) – Secret leakage through CodeBuild environments or artifacts.
🕳️ [detection_evasion](cloudgoat/cloudgoat_detection_evasion.md) – Techniques for evading CloudTrail or other monitoring services.
🕳️ [ecs_efs_attack](cloudgoat/cloudgoat_ecs_efs_attack.md) – Compromise via ECS mounting EFS volumes insecurely.

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
