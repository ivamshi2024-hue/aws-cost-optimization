# aws-cost-optimization
aws-cost-optimization-lambda

** Overview**

This project demonstrates a serverless cost optimization solution in AWS using Lambda.

In many real-world scenarios, unused EBS volumes and outdated snapshots continue to incur costs even after EC2 instances are terminated. This solution automatically identifies such unused resources and performs cleanup actions to reduce unnecessary cloud expenditure.

The system is fully automated using AWS Lambda and triggered periodically using CloudWatch Events.


 **Problem**

In AWS environments, it is common to leave behind:

- Unattached EBS volumes
- Old or unused EBS snapshots

These resources are chargeable and can lead to unnecessary costs if not monitored and cleaned regularly.

Manual cleanup is inefficient and error-prone, especially in large-scale environments.


 **Solution**

This project uses AWS Lambda to:

- Identify unused (unattached) EBS volumes
- Detect outdated or unused EBS snapshots
- Delete or log these resources based on configuration
- Send notifications using SNS (optional)

The Lambda function is triggered automatically at scheduled intervals using CloudWatch Events, ensuring continuous monitoring and cost optimization.


 **Architecture**

CloudWatch Event Rule → Lambda Function → EC2 (EBS/Snapshots) → SNS (Optional Alerts)

**AWS Services Used
**- AWS Lambda – Serverless compute to run cleanup logic
- Amazon CloudWatch – Scheduling and monitoring
- Amazon EC2 – EBS volumes and snapshots management
- Amazon SNS – Notifications and alerts
- IAM – Roles and permissions for Lambda execution

**How It Works**
1. A CloudWatch Event Rule triggers the Lambda function at a scheduled interval.
2. The Lambda function uses AWS SDK (boto3) to:
   - Fetch all EBS volumes
   - Identify volumes that are not attached to any EC2 instance
3. It then checks for EBS snapshots:
   - Filters snapshots based on age or usage
4. Based on the configuration:
   - Deletes unused volumes and snapshots OR
   - Logs them for review (safe mode)
5. Optionally, sends alerts via SNS to notify the user.

 **Features**

- Automated detection of unused EBS volumes
- Cleanup of outdated EBS snapshots
- Scheduled execution using CloudWatch
- Optional SNS notifications
- Supports safe mode (log-only without deletion)


**Prerequisites**

- AWS Account
- Basic knowledge of AWS services
- IAM role with permissions:
  - ec2:DescribeVolumes
  - ec2:DeleteVolume
  - ec2:DescribeSnapshots
  - ec2:DeleteSnapshot
  - sns:Publish

**Setup Instructions**
1. Create an IAM Role for Lambda with required permissions.
2. Create a Lambda function and upload the Python script.
3. Configure environment variables (optional for customization).
4. Create a CloudWatch Event Rule to trigger Lambda periodically.
5. (Optional) Create an SNS topic and subscribe your email.
6. Test the Lambda function manually before enabling automation.

 **Sample Use Case**

An organization frequently launches and terminates EC2 instances during testing.

After termination:
- EBS volumes remain unattached
- Snapshots accumulate over time

This Lambda solution automatically cleans up these unused resources, helping reduce AWS costs.

**Learning Outcomes**
- Hands-on experience with AWS Lambda
- Understanding of AWS cost optimization strategies
- Working with boto3 SDK for resource management
- Automating cloud operations using CloudWatch
- Implementing serverless architecture

 **Future Enhancements**

- Tag-based filtering for selective cleanup
- Email alert customization
- Integration with AWS Budgets
- Dashboard for monitoring cost savings


## Credits

Inspired by AWS DevOps Zero to Hero series by iam-veeramalla.
