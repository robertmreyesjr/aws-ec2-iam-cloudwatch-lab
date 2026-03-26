# aws-ec2-iam-cloudwatch-lab
AWS hands-on lab deploying an EC2 Apache web server with IAM role-based access, CloudWatch monitoring, and SNS email alerts for CPU and disk thresholds.
## Project Overview
This lab demonstrates how to deploy a basic Apache web server on Amazon EC2, attach an IAM role to the instance instead of using access keys, install the CloudWatch Agent to publish disk usage metrics, and configure CloudWatch alarms with SNS email notifications.

This project reflects a real-world AWS operations workflow involving compute, identity and access management, monitoring, and alerting.

---

## What I Built
I built an Amazon EC2 instance running Apache, attached an IAM role to the instance for AWS permissions, installed the CloudWatch Agent for disk monitoring, and created CloudWatch alarms that send SNS email alerts when CPU or disk usage crosses a threshold.

---

## Why I Built It
I built this lab to practice core AWS operational tasks that appear frequently in cloud support and cloud engineering roles:
- Launching and configuring EC2 instances
- Using IAM roles instead of hardcoded access keys
- Monitoring server health with CloudWatch
- Sending automatic alerts with SNS

This project helped reinforce secure access design and basic cloud monitoring concepts.

---

## AWS Services Used
- Amazon EC2
- AWS Identity and Access Management (IAM)
- Amazon CloudWatch
- Amazon SNS
- Apache HTTP Server

---

## Architecture
- A public EC2 instance hosts an Apache web server
- An IAM role is attached to the EC2 instance
- CloudWatch collects CPU metrics by default
- CloudWatch Agent publishes disk usage metrics
- CloudWatch alarms monitor CPU and disk usage
- SNS sends an email alert when an alarm enters the ALARM state

---

## Implementation Steps

### 1. Launch EC2 Instance
- Launched an Amazon Linux EC2 instance
- Allowed:
  - SSH from my IP
  - HTTP from the internet
- Confirmed the instance reached running state

### 2. Install and Configure Apache
- Connected to the instance
- Installed Apache
- Enabled and started the service
- Created a simple test homepage
- Verified the website loaded in a browser using the public IP

### 3. Create and Attach IAM Role
- Created an IAM role for EC2
- Attached these policies:
  - AmazonSSMManagedInstanceCore
  - CloudWatchAgentServerPolicy
- Attached the IAM role to the EC2 instance

### 4. Install CloudWatch Agent
- Installed the CloudWatch Agent on the instance
- Created a configuration file to collect disk usage for the root filesystem
- Started the agent and verified it was running

### 5. Create SNS Topic and Subscription
- Created an SNS topic for alerts
- Added my email address as a subscription endpoint
- Confirmed the subscription through email

### 6. Create CloudWatch Alarms
- Created a CPUUtilization alarm
- Created a disk_used_percent alarm using CloudWatch Agent metrics
- Configured both alarms to send notifications to the SNS topic

### 7. Validate the Monitoring Setup
- Generated CPU load on the instance
- Created a large temporary file to raise disk usage
- Confirmed alarm state changes in CloudWatch
- Confirmed SNS email notifications were received

---

## Validation
I validated the solution by confirming:
- The Apache web server loaded successfully in a browser
- The EC2 instance had the IAM role attached
- The CloudWatch Agent was running
- The `disk_used_percent` metric appeared in CloudWatch
- CloudWatch alarms changed state when usage thresholds were exceeded
- SNS email alerts were delivered successfully

---

## Screenshots

### 1. EC2 Launch Configuration
Shows:
- Instance name
- AMI
- Instance type
- Security group rules

### 2. Apache Web Server Running
Shows:
- Browser open to the EC2 public IP
- Test webpage loading successfully

### 3. IAM Role Created
Shows:
- Role name
- Trusted entity as EC2
- Attached policies

### 4. IAM Role Attached to EC2
Shows:
- EC2 instance details
- IAM role field with attached role

### 5. CloudWatch Agent Running
Shows:
- Terminal output with CloudWatch Agent active/running

### 6. SNS Subscription Confirmed
Shows:
- SNS topic page or email confirmation

### 7. CPU Alarm Created
Shows:
- CPUUtilization alarm details
- Threshold and SNS action

### 8. Disk Alarm Created
Shows:
- disk_used_percent alarm details
- Threshold and SNS action

### 9. Alarm Triggered / Email Received
Shows:
- CloudWatch alarm state as ALARM
- Or SNS alert email

### 10. Architecture Diagram
Shows:
- User
- EC2 web server
- IAM role
- CloudWatch
- SNS
- Email alert path

---

## What I Learned
- IAM roles are the preferred way to grant AWS permissions to EC2 instances
- EC2 CPU metrics are available by default in CloudWatch
- Disk usage monitoring requires the CloudWatch Agent
- CloudWatch alarms and SNS provide a simple but effective alerting workflow
- Monitoring and alerting are core parts of day-to-day cloud operations

---

## Free Tier / Cost Notes
This lab can be done within AWS Free Tier limits if small, eligible resources are used and the environment is cleaned up promptly. Some monitoring features may incur small charges depending on account type and usage, so it is important to review the AWS Billing dashboard and remove resources after testing.

---

## Cleanup
To avoid ongoing charges, I cleaned up the following resources after completing the lab:
- Terminated the EC2 instance
- Deleted the CloudWatch alarms
- Deleted the SNS topic and subscription
- Removed the IAM role if no longer needed

---

## Repository Structure

```text
aws-ec2-iam-cloudwatch-lab/
├── README.md
├── build-steps.md
├── architecture-diagram.png
└── screenshots/
    ├── 01-ec2-launch.png
    ├── 02-web-server-running.png
    ├── 03-iam-role.png
    ├── 04-role-attached-to-ec2.png
    ├── 05-cloudwatch-agent-running.png
    ├── 06-cpu-alarm.png
    ├── 07-disk-alarm.png
    ├── 08-sns-subscription-confirmed.png
    ├── 09-alarm-state-or-email-alert.png
    └── 10-architecture-diagram.png
