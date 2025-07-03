# 🔐 AWS Cloud Security Implementation

---

## 🎯 Objective

The objective of this project is to apply essential cloud security practices on Amazon Web Services (AWS) that ensure secure data storage, fine-grained access control, and resource integrity. It utilizes IAM, Amazon S3, and EC2 to demonstrate encryption, access management, and versioning based on industry security standards.

---

## 🧰 Tools and Services Used

- **Amazon EC2** – Virtual compute instance
- **Amazon S3** – Secure storage with versioning and encryption
- **AWS IAM** – Identity and Access Management for role-based permissions
- **Amazon Linux 2** – OS for EC2 instance
- **AWS Console** – Web interface for setup

---

## 🔐 IAM Role-Based Access Control

**Role Name:** `SecureAccessEC2Role`  
**Attached Policies:**
- `AmazonS3ReadOnlyAccess`
- `CloudWatchAgentServerPolicy` *(optional)*

**Steps:**
1. Go to **IAM → Roles → Create Role**
2. Select **AWS Service → EC2**
3. Attach above policies
4. Name the role and create it

---

## 🖥️ Assign IAM Role to EC2

1. Open **EC2 → Instances**
2. Choose instance (e.g., `secure-instance`)
3. Actions → Security → Modify IAM Role
4. Select `SecureAccessEC2Role` and attach

---

## 📦 Secure S3 Bucket with Encryption & Versioning

**Bucket Name:** `encrypted-versioned-bucket`  
**Encryption:** Enabled (SSE-S3)  
**Versioning:** Enabled  
**Public Access:** Blocked

**Steps:**
1. Go to **S3 → Create Bucket**
2. Name it and choose region
3. Enable encryption & versioning
4. Block all public access
5. Create bucket

---

## 📁 File Upload with Encryption and Versioning

1. Open the bucket
2. Upload `confidential.txt`
3. Confirm **encryption** is enabled
4. Upload a modified version to test **versioning**

---

## 📜 Custom IAM Policy

**Policy Name:** `RestrictedS3Policy`

json code:
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowOnlyListing",
      "Effect": "Allow",
      "Action": ["s3:ListBucket"],
      "Resource": ["arn:aws:s3:::encrypted-versioned-bucket"]
    },
    {
      "Sid": "AllowReadWriteOnObjects",
      "Effect": "Allow",
      "Action": ["s3:GetObject", "s3:PutObject"],
      "Resource": ["arn:aws:s3:::encrypted-versioned-bucket/*"]
    }
  ]
}

---

## 📝 Steps to Implement IAM Policy
Go to IAM → Policies → Create
Paste the above JSON in the JSON tab
Name the policy: RestrictedS3Policy
Attach to the IAM Role

---

## 🧪 Test Permissions Code (Optional via AWS CLI)
aws s3 ls s3://encrypted-versioned-bucket/
aws s3 cp confidential.txt s3://encrypted-versioned-bucket/

---

## 📷 Screenshots
Place the following screenshots in a folder named screenshots/:

IAM Role Configuration

EC2 Instance with Attached Role

S3 Bucket Encryption and Versioning Settings

Upload Confirmation Screenshot

Version History View

---

## 📚 Key Takeaways
IAM roles allow secure instance access without using access keys

S3 encryption and versioning protect sensitive data and enable recovery

Custom IAM policies enforce least privilege and better access control

The configuration is secure, scalable, and ready for production

---

## ✅ Conclusion
This configuration demonstrates an end-to-end AWS-based security architecture.
It leverages IAM for access control, EC2 for compute, and S3 for secure and versioned storage.
These practices are essential for implementing robust cloud security and compliance.

---

