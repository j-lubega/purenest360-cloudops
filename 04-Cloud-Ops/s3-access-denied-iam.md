# Troubleshooting S3 "Access Denied"
**Scenario:** An EC2 instance with an IAM role cannot write files to an S3 bucket.

### 1. Investigation Steps
* **Check IAM Policy:** Does the role have `s3:PutObject` permissions?
* **Check Bucket Policy:** Does the S3 bucket have a policy that explicitly "Denies" access? (Deny always wins).
* **KMS Encryption:** Is the bucket encrypted with a KMS key? If so, the IAM role needs `kms:GenerateDataKey` permissions.

### 2. The Fix
* Update the IAM role to include the specific bucket ARN.
* Ensure the VPC Endpoint (if used) allows traffic to S3.
