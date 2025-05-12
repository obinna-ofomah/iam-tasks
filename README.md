# AWS IAM Policy Tasks & ARN Reference

This repository contains three tasks demonstrating the practical use of AWS Identity and Access Management (IAM) policies. These tasks showcase permission control for S3 resources, IAM user creation, and how to format Amazon Resource Names (ARNs) for use in IAM policies.

---

## 🧾 Task 1: S3 Bucket Access with Conditional Permissions

This IAM policy grants and denies specific permissions for Amazon S3 buckets and objects. It illustrates how to implement fine-grained access control over S3 resources using both `Allow` and `Deny` statements.

### 📜 Policy Breakdown
- Allows listing of **all S3 buckets**.
- Allows listing of **specific buckets** that contain `"spark-job"` in their name.
- Allows **deletion of objects** under a specific folder path: `spark-job-data-input/dumps/*`.
- Explicitly **denies deletion of `.csv` files** in the same path, enforcing file-type restrictions.

  ```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Allow",
      "Action": ["s3:ListAllMyBuckets"],
      "Resource": ["*"]
    },
    {
      "Sid": "Statement2",
      "Effect": "Allow",
      "Action": ["s3:ListBucket"],
      "Resource": ["arn:aws:s3:::*spark-job*"]
    },
    {
      "Sid": "Statement3",
      "Effect": "Allow",
      "Action

---

## 👷 Task 2: IAM User Creation Restriction

This IAM policy permits creating IAM users whose names begin with the prefix `engineer`.

### 📜 Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Allow",
      "Action": ["iam:CreateUser"],
      "Resource": ["arn:aws:iam::340752803932:user/engineer*"]
    }
  ]
}

### 🔍 Summary
- Ensures that only IAM users with a naming pattern of engineer* can be created.
- Helps enforce organisational naming conventions and restrict the scope of user creation.




