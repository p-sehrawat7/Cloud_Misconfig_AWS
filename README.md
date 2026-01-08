#  Cloud Misconfiguration Lab (AWS)

A hands-on cloud security lab where I intentionally deployed insecure AWS resources to understand how real-world cloud breaches happen—and how to detect and fix them.

---

##  Overview

This project demonstrates how common AWS misconfigurations can lead to data exposure, how attackers abuse them, and how defenders remediate and detect such issues.

**Focus areas:**
- S3 public access via bucket policy
- Over-permissive IAM roles
- EC2 exposure
- Risk-based remediation
- Detection using CloudTrail

All activities were performed safely inside a personal AWS lab account.

---

## Architecture (High Level)

- IAM users & roles (least privilege vs over-permission)
- S3 bucket (intentionally public → secured)
- EC2 instance (public exposure)
- CloudTrail (detection & audit)

---

##  Phase 1 — IAM Setup
- Created restricted IAM user (`lab-user`)
- Created admin group for emergency use
- Enabled MFA
- Applied least-privilege permissions

**Learning:** IAM misconfiguration is a primary cause of cloud breaches.

---

##  Phase 2 — Intentional Misconfigurations

### Part A: Public S3 Bucket
- Disabled Block Public Access
- Added a public bucket policy
- Exposed an object publicly

**Impact:** Anyone on the internet could read bucket objects.

### Part B: EC2 Exposure
- Launched a public EC2 instance
- Attached an over-permissive IAM role (`s3:*`)
- Exposed SSH/HTTP publicly

**Note:** Metadata exploitation was restricted due to IMDSv2, demonstrating layered defenses.

---

##  Phase 3 — Remediation (Risk-Based)

### S3 Fixes
- Removed public bucket policy
- Enforced S3 Block Public Access

> Object-level ACL migration was intentionally skipped to avoid risky changes. Public exposure was mitigated using layered controls—reflecting real-world, risk-based remediation.

### IAM Fixes
- Removed over-permissive policies
- Applied least-privilege access

### EC2 Fixes
- Restricted security group access
- Verified IMDSv2 enforcement

---

##  Phase 4 — Detection & Logging

- Used **CloudTrail Event History** to investigate:
  - `PutBucketPolicy`
  - `DeleteBucketPolicy`
  - S3 access events
- Analyzed event details including:
  - User identity
  - Source IP
  - Timestamp
  - Request parameters

**Learning:** Every risky action leaves an audit trail—defenders rely on these logs.

---

##  Key Security Takeaways

- Public S3 access can occur via multiple paths (policies, ACLs).
- Least privilege must be combined with metadata hardening.
- Detection is as important as prevention.
- Risk-based remediation is often safer than aggressive changes.

---

##  Skills Demonstrated

- AWS IAM & S3 security
- Cloud misconfiguration analysis
- Defensive cloud security mindset
- CloudTrail investigation
- Professional documentation

---

#  Cloud Misconfiguration Lab (AWS)

A hands-on cloud security lab where I intentionally deployed insecure AWS resources to understand how real-world cloud breaches happen—and how to detect and fix them.

---

##  Overview

This project demonstrates how common AWS misconfigurations can lead to data exposure, how attackers abuse them, and how defenders remediate and detect such issues.

**Focus areas:**
- S3 public access via bucket policy
- Over-permissive IAM roles
- EC2 exposure
- Risk-based remediation
- Detection using CloudTrail

All activities were performed safely inside a personal AWS lab account.

---

## Architecture (High Level)

- IAM users & roles (least privilege vs over-permission)
- S3 bucket (intentionally public → secured)
- EC2 instance (public exposure)
- CloudTrail (detection & audit)

---

##  Phase 1 — IAM Setup
- Created restricted IAM user (`lab-user`)
- Created admin group for emergency use
- Enabled MFA
- Applied least-privilege permissions

**Learning:** IAM misconfiguration is a primary cause of cloud breaches.

---

##  Phase 2 — Intentional Misconfigurations

### Part A: Public S3 Bucket
- Disabled Block Public Access
- Added a public bucket policy
- Exposed an object publicly

**Impact:** Anyone on the internet could read bucket objects.

### Part B: EC2 Exposure
- Launched a public EC2 instance
- Attached an over-permissive IAM role (`s3:*`)
- Exposed SSH/HTTP publicly

**Note:** Metadata exploitation was restricted due to IMDSv2, demonstrating layered defenses.

---

##  Phase 3 — Remediation (Risk-Based)

### S3 Fixes
- Removed public bucket policy
- Enforced S3 Block Public Access

> Object-level ACL migration was intentionally skipped to avoid risky changes. Public exposure was mitigated using layered controls—reflecting real-world, risk-based remediation.

### IAM Fixes
- Removed over-permissive policies
- Applied least-privilege access

### EC2 Fixes
- Restricted security group access
- Verified IMDSv2 enforcement

---

##  Phase 4 — Detection & Logging

- Used **CloudTrail Event History** to investigate:
  - `PutBucketPolicy`
  - `DeleteBucketPolicy`
  - S3 access events
- Analyzed event details including:
  - User identity
  - Source IP
  - Timestamp
  - Request parameters

**Learning:** Every risky action leaves an audit trail—defenders rely on these logs.

---

##  Key Security Takeaways

- Public S3 access can occur via multiple paths (policies, ACLs).
- Least privilege must be combined with metadata hardening.
- Detection is as important as prevention.
- Risk-based remediation is often safer than aggressive changes.

---

##  Skills Demonstrated

- AWS IAM & S3 security
- Cloud misconfiguration analysis
- Defensive cloud security mindset
- CloudTrail investigation
- Professional documentation

---

### CLI Commands Used

```bash
aws s3api get-bucket-policy --bucket lab-vuln-bucket-priyansh
aws s3 ls s3://lab-vuln-bucket-priyansh
curl https://lab-vuln-bucket-priyansh.s3.amazonaws.com/secret.txt
```

---

##  Disclaimer
This project was conducted in a controlled lab environment for educational purposes only.

