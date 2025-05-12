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

---
