# AWS CloudWatch Monitoring Lab

## Project Overview

This project focused on building a basic AWS monitoring and alerting environment using Amazon CloudWatch. The goal was to monitor an EC2 Linux instance, collect operating system logs, track resource utilization, and configure alarms that send email notifications when resource thresholds are exceeded.

The project provided hands-on experience with AWS monitoring, centralized logging, Systems Manager, IAM roles, and automated alerting.

## Architecture

The lab used an Amazon EC2 instance running Amazon Linux 2023 as the monitored server.

The monitoring architecture included:

- **Amazon EC2:** Hosted the Linux environment being monitored.
- **Amazon CloudWatch:** Collected metrics, stored logs, displayed dashboards, and evaluated alarms.
- **CloudWatch Agent:** Collected operating system logs, memory utilization, and disk utilization.
- **AWS Systems Manager:** Installed and configured the CloudWatch Agent remotely using Run Command.
- **Amazon SNS:** Delivered email notifications when CloudWatch alarms entered the ALARM state.

## Project Implementation

### 1. EC2 Instance Setup

- Launched a temporary Amazon Linux 2023 EC2 instance.
- Configured a `t3.micro` instance for monitoring exercises.
- Verified that the instance was running and publishing basic CloudWatch metrics.
- Located the EC2 CPU utilization metric within the AWS/EC2 namespace.

### 2. CPU Monitoring and Alarms

- Located and reviewed the CPUUtilization metric.
- Created a CloudWatch alarm named `cloudwatch-ec2-high-cpu`.
- Configured the alarm to trigger when average CPU utilization exceeded 80%.
- Reviewed CloudWatch alarm states: OK, ALARM, and INSUFFICIENT_DATA.

### 3. SNS Email Notifications

- Created an SNS topic named `cloudwatch-cpu-alerts`.
- Configured and confirmed an email subscription.
- Connected the SNS topic to the CloudWatch CPU alarm.
- Established an automated notification workflow when an alarm enters the ALARM state.

### 4. CloudWatch Dashboard

Created a dashboard named `cloudwatch-monitoring-dashboard` to centralize monitoring information.

Added widgets for:

- EC2 CPU utilization.
- CPU alarm status.
- Memory utilization.
- Disk utilization.

### 5. CloudWatch Logs and Agent Installation

Created an IAM role named `CloudWatchMonitoringEC2Role` and attached the following AWS managed policies:

- `AmazonSSMManagedInstanceCore`
- `CloudWatchAgentServerPolicy`

Attached the role to the EC2 instance and used AWS Systems Manager Run Command to install the Amazon CloudWatch Agent.

Configured the agent to collect Linux system logs from:

`/var/log/cloud-init-output.log`

Configured the agent to send the logs to the CloudWatch Log Group:

`/aws/ec2/cloudwatch-monitoring-lab`

Verified that log streams and log events were successfully received in CloudWatch Logs.

### 6. Memory and Disk Monitoring

Updated the CloudWatch Agent configuration to collect additional operating system metrics.

Configured:

- `mem_used_percent` — monitors RAM utilization.
- `disk_used_percent` — monitors filesystem storage utilization.

Published these metrics under the custom CloudWatch namespace:

`CWAgent`

Verified that both metrics were available in the CloudWatch Metrics console.

### 7. Memory and Disk Alarms

Created two additional CloudWatch alarms:

- `cloudwatch-ec2-high-memory`
- `cloudwatch-ec2-high-disk`

Configured both alarms to trigger when average utilization exceeded 80%.

Connected both alarms to the existing SNS topic for email notifications.

## Screenshots

The following screenshots provide visual evidence of the completed CloudWatch monitoring environment:

- **CloudWatch Dashboard:** Displays CPU, memory, disk utilization, and alarm status.
- **CloudWatch Alarms:** Shows the configured CPU, memory, and disk monitoring alarms.
- **CloudWatch Logs:** Demonstrates Linux log events successfully delivered from the EC2 instance.
- **CloudWatch Agent Metrics:** Shows custom memory and disk metrics published under the CWAgent namespace.

Screenshots are available in the `screenshots/` directory.

## Configuration Files

The `configs/` directory contains the CloudWatch Agent configuration used during this project.

- `amazon-cloudwatch-agent.json` — Defines Linux log collection, memory utilization metrics, and disk utilization metrics.

This configuration can serve as a starting point for deploying CloudWatch Agent monitoring on additional EC2 instances.



## Skills and AWS Services Practiced

- Amazon CloudWatch metrics, logs, alarms, and dashboards
- CloudWatch Agent installation and configuration
- Amazon EC2 administration
- AWS Systems Manager Run Command
- AWS IAM roles and managed policies
- Amazon SNS email notifications
- Linux log files and operating system monitoring
- Custom CloudWatch metrics and namespaces
- Resource utilization monitoring and alerting

## Project Outcome

Successfully built a basic centralized monitoring environment for an AWS EC2 instance.

Configured CloudWatch to monitor CPU, memory, and disk utilization, collect Linux operating system logs, and provide automated email notifications through SNS.

This project reinforced how cloud engineers monitor infrastructure health, identify potential resource issues, centralize system logs, and configure alerts to help prevent service interruptions.


