# AWS Cloud Cost Optimization – Stale EBS Snapshot Cleanup

This AWS Lambda function identifies and deletes **stale EBS snapshots** that are no longer associated with any active EC2 instances, helping reduce unnecessary **EBS storage costs**.

---

## 📌 Overview

EBS snapshots are great for backup and recovery, but unused snapshots can accumulate and inflate your AWS bill. This Lambda function automates the cleanup process by:

- Fetching all EBS snapshots owned by your account.
- Retrieving all active EC2 instances (running or stopped).
- Identifying snapshots whose source volumes are no longer in use.
- Deleting those stale snapshots.

---

## How It Works

1. **List EBS Snapshots** owned by your AWS account.
2. **List Active EC2 Instances** (states: running or stopped).
3. **Check for Usage**: Match snapshots’ source volume IDs with the volumes in use.
4. **Delete** any snapshot where the volume is not attached to an active instance.

---

## Deployment

### Prerequisites

- AWS Lambda function with Python runtime (e.g., 3.9+)
- IAM Role with permissions:
  - `ec2:DescribeSnapshots`
  - `ec2:DescribeInstances`
  - `ec2:DeleteSnapshot`

### Steps

1. Create a new Lambda function in AWS.
2. Assign the required IAM role.
3. Upload or paste the function code.
4. (Optional) Schedule the function using Amazon EventBridge to run periodically.

---

## Warnings

- **This function permanently deletes EBS snapshots.**
- Ensure that critical snapshots are protected (e.g., using tags).
- Consider implementing a **dry-run** mode or email/SNS reports before enabling automatic deletion.

---

## Conclusion

Managing AWS costs efficiently requires continuous monitoring and cleanup of unused resources. This Lambda function helps automate the identification and deletion of stale EBS snapshots, which can silently accumulate over time and increase your monthly bill. By integrating this into your cloud cost optimization strategy, you can ensure better resource hygiene, reduce waste, and save money—without compromising on availability or data protection.

Take control of your AWS costs—automate wisely.
