# Cloud Misconfiguration Lab (AWS, IAM)

This project is a hands-on lab where I intentionally deploy and analyze common AWS misconfigurations.  
The goal is to understand how these mistakes occur, how attackers exploit them, and how to properly secure cloud environments.

---

## Overview

This lab covers:

- Public S3 bucket misconfiguration  
- Over-permissive IAM roles  
- EC2 Instance Metadata exploitation  
- Least privilege principles  
- Logging and detection using CloudTrail  

All testing is performed inside a dedicated AWS lab account.

---

## Phase 1 — IAM Setup (Completed)

### IAM Groups
- **Admins-lab** – administrative/emergency use  
- **Lab-Developers** – least-privilege group for day-to-day access  

### IAM User
- Username: `lab-user`  
- Access: Console + Programmatic  
- MFA enabled  

### Security Controls
- Billing alerts enabled  
- Password policy enforced  
- CloudTrail logging configured  

---

## Phase 2 — Public S3 Bucket Misconfiguration (Completed)

### Bucket Details
- Name: `lab-vuln-bucket-priyansh`  
- Region: `ap-south-1`  
- Object Ownership: ACLs enabled  
- Block Public Access: disabled  
- ACL: public read access granted  

### Exposed File
- `secret.txt`  
- The file was publicly accessible without authentication  

### CLI Commands Used

```bash
aws s3api get-bucket-policy --bucket lab-vuln-bucket-priyansh
aws s3 ls s3://lab-vuln-bucket-priyansh
curl https://lab-vuln-bucket-priyansh.s3.amazonaws.com/secret.txt


Due to existing legacy object ACLs, bucket-owner-enforced mode was not enabled. Instead, public exposure was mitigated by removing public bucket policies and enforcing S3 Block Public Access, demonstrating a risk-based remediation approach commonly used in production environments.

CloudTrail event details were analyzed to trace S3 configuration changes, including bucket policy modifications. The logs provide user identity, source IP, and request parameters, enabling accurate detection and investigation of risky actions.
