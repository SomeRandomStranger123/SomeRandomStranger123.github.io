
# 🛠️ Incident Analysis: Tracing a Suspicious User in AWS Logs

## ⚡ TL;DR

A suspicious user named `temp-user` was discovered in CloudTrail logs. Through enumeration, we identified that:

- The user authenticated from an external IP.
- Multiple failed attempts were made, followed by privilege escalation via `AssumeRole` into an Admin role.
- The attacker then used their elevated access to exfiltrate a file (`emergency.txt`) from an S3 bucket.
- We validated each step using PowerShell, `jq`, and confirmed the final path with the AWS CLI.

---

## 🧠 Skills Involved

- Prettifying JSON files for easier analysis  
- Familiarity with the AWS CLI  
- Familiarity with analyzing CloudTrail logs  
- Enumerating S3 buckets  
- Simulating an attacker to validate the path to breach  

---

## 📂 Step 1: Prettifying JSON for Better Readability

The raw CloudTrail logs were difficult to read. We used the following tools to format them properly.

### **Using `jq` (Linux/macOS/WSL)**

```bash
for file in *.json; do jq . "$file" > "$file.tmp" && mv "$file.tmp" "$file"; done
```

✅ JSON is now indented and easy to parse in a text editor.

---

### **Using PowerShell (Windows)**

```powershell
Get-ChildItem *.json | ForEach-Object {
    $json = Get-Content $_.FullName | ConvertFrom-Json
    $json | ConvertTo-Json -Depth 100 | Set-Content $_.FullName
}
```

✅ Same result on Windows.
![image (4)](https://github.com/user-attachments/assets/c29f70f6-8933-4a42-8edc-ce25a7bd90c1)
---

## 🔍 Step 2: Enumerate Active Users from Logs

### **Using `grep`**

```bash
grep -r userName | sort -u
```

### **PowerShell Equivalent**

```powershell
Get-ChildItem -Recurse -File | 
    Select-String -Pattern "userName" | 
    ForEach-Object { $_.Line } | 
    Sort-Object -Unique
```



![image (5)](https://github.com/user-attachments/assets/700a61d5-97b7-4991-99af-742a4edc42cb)

This reveals the suspicious username `temp-user` that doesn’t match internal naming conventions.


---

## 🧾 Step 3: Investigate Actions of `temp-user`

```powershell
Get-ChildItem -Recurse -File |
ForEach-Object {
    $lines = Get-Content $_.FullName
    for ($i = 0; $i -lt $lines.Count; $i++) {
        if ($lines[$i] -match "temp-user") {
            $end = [math]::Min($i + 10, $lines.Count - 1)
            for ($j = $i; $j -le $end; $j++) {
                $lines[$j]
            }
            ""
        }
    }
}
```

![image (6)](https://github.com/user-attachments/assets/b5fba224-bfb7-493d-853d-3ded764b9558)
![image (7)](https://github.com/user-attachments/assets/806fb1a7-07b6-4436-85ba-fc4a103266ad)

We see multiple failed activity attempts — likely early enumeration.

---

## 🕵️ Step 4: Tracing the Source IP

```json
"eventName": "GetCallerIdentity",
"sourceIPAddress": "84.32.71.19",
"userName": "temp-user",
"arn": "arn:aws:iam::107513503799:user/temp-user"
```



We can `whois` or `curl` the IP to investigate its source.
![image (8)](https://github.com/user-attachments/assets/b0f7a011-b378-44d3-8cd2-07d5a97d2a8c)

---

## 📝 Step 5: Export All Matches to a File

```powershell
Get-ChildItem -Recurse -File |
    ForEach-Object {
        $lines = Get-Content $_.FullName
        for ($i = 0; $i -lt $lines.Count; $i++) {
            if ($lines[$i] -match "temp-user") {
                $end = [math]::Min($i + 10, $lines.Count - 1)
                for ($j = $i; $j -le $end; $j++) {
                    $lines[$j]
                }
                ""
            }
        }
    } | Out-File "matches.txt" -Encoding UTF8
```

✅ `matches.txt` contains all activity around `temp-user`.

---

## 🚨 Step 6: Privilege Escalation Found

```json
 "userName":  "temp-user"                     },
 "eventTime":  "2023-08-26T20:54:28Z",
 "eventSource":  "sts.amazonaws.com",
 "eventName":  "AssumeRole",
 "awsRegion":  "us-east-1",
 "sourceIPAddress":  "84.32.71.33",
 "userAgent":  "aws-cli/1.27.74 Python/3.10.6 Linux/5.15.90.1-microsoft-standard-WSL2 botocore/1.29.74",
 "requestParameters":  {
 "roleArn":  "arn:aws:iam::107513503799:role/AdminRole",
Confirms elevation from `temp-user` to `AdminRole`.
```
---

## 🔎 Step 7: Filter by IP, Exclude AccessDenied

```powershell
$output = @()
$targetIP = "84.32.71.3"

Get-ChildItem -Recurse -File -Include *.json | ForEach-Object {
    try {
        $json = Get-Content $_.FullName -Raw | ConvertFrom-Json
        foreach ($entry in $json) {
            $entryText = $entry | ConvertTo-Json -Depth 10
            if ($entryText -match [regex]::Escape($targetIP) -and $entryText -notmatch "AccessDenied") {
                $output += $entryText
                $output += ""
            }
        }
    } catch {
        Write-Host "Failed to parse: $($_.FullName)"
    }
}

$output | Out-File "filtered_output.txt" -Encoding UTF8
```

---

## 💾 Step 8: Data Exfiltration Identified

```json
"eventName": "GetObject",
"bucketName": "emergency-data-recovery",
"key": "emergency.txt",
"bytesTransferredOut": 2232,
"sourceIPAddress": "84.32.71.3"
```


## ✅ Validation: Simulating the Attack Path with AWS CLI

To simulate and confirm this path in a safe test environment, we can mirror the attacker’s behavior using AWS CLI commands.

### **1. Authenticate with AWS credentials**
```bash
aws configure
```

### **2. Run `GetCallerIdentity` as temp-user**
```bash
aws sts get-caller-identity --profile temp-user
```

Expected output:
```json
{
  "UserId": "AIDAEXAMPLE",
  "Account": "107513503799",
  "Arn": "arn:aws:iam::107513503799:user/temp-user"
}
```

### **3. Assume Role into AdminRole**
```bash
aws sts assume-role   --role-arn arn:aws:iam::107513503799:role/AdminRole   --role-session-name attackerSession   --profile temp-user
```

Store and export the temporary credentials from this response.

### **4. Access the sensitive file in S3**
```bash
aws s3 cp s3://emergency-data-recovery/emergency.txt ./emergency.txt   --region us-east-1   --profile attackerSession
```

✅ This mimics the attacker successfully accessing `emergency.txt`.
