# ☁️ CloudGoat Scenarios (Ranked: Easy ➜ Hard)

✅ = Completed  
🔄 = In Progress  
🔒 = Not Started  

---

## 🟢 Easy

✅ [beanstalk_secrets](cloudgoat/cloudgoat_beanstalk_secrets.md)  
*Exploit Beanstalk environment variables to pivot to admin.*

✅ [sns_secrets](cloudgoat/cloudgoat_sns_secrets.md)  
*Subscribe to SNS topic, leak API key, access final flag.*

✅ [lambda_privesc](cloudgoat/cloudgoat_lambda_privesc.md)  
*Assume Lambda role, use pass-role permissions to escalate.*

🔒 iam_privesc_by_key_rotation  
*Rotate access keys and abuse privilege over IAM users.*

🔒 iam_privesc_by_rollback  
*Restore an older IAM policy to gain admin rights.*

🔒 sqs_flag_shop  
*Source code analysis to exploit a vulnerable SQS-based shop.*

---

## 🟡 Medium

🔒 vulnerable_cognito  
*Bypass Cognito sign-up/login to access Identity Pool credentials.*

🔒 vulnerable_lambda  
*Exploit broken Lambda function to escalate user privileges.*

🔒 cloud_breach_s3  
*Use SSRF against EC2 metadata → exfiltrate sensitive S3 data.*

🔒 iam_privesc_by_attachment  
*Attach new instance profiles to gain escalated EC2 access.*

🔒 ec2_ssrf  
*Exploit SSRF in EC2 webapp to gain Lambda-level access.*

🔒 ecs_takeover  
*Find RCE in webapp, abuse ECS misconfig to reschedule compromised containers.*

🔒 rds_snapshot  
*Steal credentials and use RDS snapshot to pull flag.*

🔒 glue_privesc  
*Exploit SQLi, reverse shell into AWS Glue, retrieve secrets.*

---

## 🔴 Hard

🔒 rce_web_app  
*Exploit webapp and multiple AWS services to access secure RDS.*

🔒 codebuild_secrets  
*Find IAM keys in CodeBuild, pivot through multiple users and RDS snapshots.*

🔒 detection_evasion  
*Exfiltrate secrets *without triggering alerts* — stealthy red team style.*

🔒 ecs_efs_attack  
*Backdoor container, abuse EC2/ECS tags to mount EFS and extract data.*

🔄 secrets_in_the_cloud  
*Chain misconfigs across many AWS services to retrieve final secret.*

---

📌 **Progress:** 3 / 20 completed, 1 in progress
