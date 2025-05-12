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

This IAM policy permits the creation of IAM users whose names begin with the prefix `engineer`.

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


## 🧱 Task 3: ARN Formats for AWS Resources

This section provides a reference guide for constructing **Amazon Resource Names (ARNs)** across various AWS services. ARNs uniquely identify AWS resources and are critical for defining precise IAM policies.

### 🔗 Official AWS Documentation

- [S3 Resources ARN Reference](https://docs.aws.amazon.com/service-authorization/latest/reference/list_amazons3.html#amazons3-resources-for-iam-policies)
- [IAM Resources ARN Reference](https://docs.aws.amazon.com/service-authorization/latest/reference/list_awsidentityandaccessmanagementiam.html#awsidentityandaccessmanagementiam-resources-for-iam-policies)
- [EC2 Resources ARN Reference](https://docs.aws.amazon.com/service-authorization/latest/reference/list_amazonec2.html#amazonec2-resources-for-iam-policies)

---

### 📦 S3 ARN Formats

| Resource Type        | ARN Format                                                                 |
|----------------------|----------------------------------------------------------------------------|
| Access Point         | `arn:${Partition}:s3:${Region}:${Account}:accesspoint/${AccessPointName}` |
| Bucket               | `arn:${Partition}:s3:::${BucketName}`                                     |
| Storage Lens Group   | `arn:${Partition}:s3:${Region}:${Account}:storage-lens-group/${Name}`     |
| Object               | `arn:${Partition}:s3:::${BucketName}/${ObjectName}`                        |

---

### 👤 IAM ARN Formats

| Resource Type | ARN Format                                                             |
|---------------|------------------------------------------------------------------------|
| MFA Device    | `arn:${Partition}:iam::${Account}:mfa/${MfaTokenIdWithPath}`           |
| Role          | `arn:${Partition}:iam::${Account}:role/${RoleNameWithPath}`            |
| User          | `arn:${Partition}:iam::${Account}:user/${UserNameWithPath}`            |

---

### 🖥 EC2 ARN Formats

| Resource Type | ARN Format                                                              |
|---------------|-------------------------------------------------------------------------|
| Elastic IP    | `arn:${Partition}:ec2:${Region}:${Account}:elastic-ip/${AllocationId}`  |
| Fleet         | `arn:${Partition}:ec2:${Region}:${Account}:fleet/${FleetId}`            |
| Instance      | `arn:${Partition}:ec2:${Region}:${Account}:instance/${InstanceId}`      |
| Image         | `arn:${Partition}:ec2:${Region}::image/${ImageId}`                      |

---

### 📘 Notes

- `${Partition}` is typically `aws`, but may be `aws-cn` for China or `aws-us-gov` for GovCloud.
- Replace variables such as `${Region}`, `${Account}`, and `${BucketName}` with actual values.
- This reference helps ensure the accurate configuration of IAM policies with resource-level permissions.

