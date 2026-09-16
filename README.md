# aws-secure-cloud-environment
Secure AWS cloud environment designed using AWS security and infrastructure best practices.

AWS Secure Cloud Environment
Overview

This project demonstrates the design and implementation of a secure AWS cloud environment using AWS security and infrastructure best practices.

The environment will focus on identity and access management, network security, encryption, logging, monitoring, and security validation.

Project Goals
Implement secure identity and access management
Design a segmented AWS network
Deploy and securely configure cloud compute resources
Implement encryption and key management
Enable centralized logging and monitoring
Apply security hardening and least-privilege principles
Test and document the security of the environment
AWS Services

The project will use AWS services including:

IAM
VPC
EC2
S3
KMS
CloudTrail
CloudWatch
AWS Config
GuardDuty
Architecture

The planned environment will contain separate network components for public-facing and private resources while applying appropriate access controls between them.

An architecture diagram will be added as the project develops.

Security Principles:

This project will follow several core security principles

Least privilege
Defense in depth
Network segmentation
Encryption at rest and in transit
Centralized logging
Continuous monitoring
Secure administrative access
Regular security validation
Project Structure
architecture/       Architecture diagrams and design
documentation/      Project documentation and decisions
screenshots/        AWS configuration evidence
iam/                Identity and access management
networking/         VPC and network security
compute/             EC2 and compute configuration
logging-monitoring/ AWS logging and monitoring
encryption/         Encryption and key management
testing/            Security testing and validation
Project Status

## Day 1 — Foundation and Repository Setup

### Configuration
AWS account configured
Root account MFA enabled
IAM administrative user configured
IAM administrator group configured
Access Analyzer enabled
GitHub repository created
Project documentation structure established
Future Work

The following components will be implemented during the project:

IAM security configuration
VPC and network segmentation
Secure EC2 deployment
Encryption and logging
Monitoring and security services
Security testing
Final security review


## Day 2 – VPC & Network Security

Built a segmented AWS network architecture using a custom VPC with separate public and private subnets.

### Configuration
- Created `SecureCloud-VPC` using CIDR block `10.0.0.0/16`
- Created public subnet `10.0.1.0/24` in `us-west-2a`
- Created private subnet `10.0.2.0/24` in `us-west-2b`
- Created and attached an Internet Gateway
- Configured a public route table with internet access through the Internet Gateway
- Kept the private subnet without a direct internet route
- Created separate security groups for public and private resources
- Applied least-privilege principles by allowing no unnecessary inbound traffic

### Security Design
The environment uses network segmentation to separate public-facing resources from private resources. Internet-bound traffic from the public subnet is routed through the Internet Gateway, while the private subnet remains isolated from direct internet access.

Security groups were configured with no inbound access by default, reducing the attack surface until specific application requirements are introduced.


## Day 3 – Logging, Monitoring & Security Alerts

- Created a multi-region AWS CloudTrail trail (`SecureCloud-Trail`) to record AWS account activity and API events.
- Configured a dedicated S3 bucket for CloudTrail log storage.
- Verified S3 server-side encryption (SSE-S3) and Block Public Access.
- Integrated CloudTrail with CloudWatch Logs using `SecureCloud-CloudTrail-Logs`.
- Created the `FailedConsoleLoginFilter` metric filter to detect failed AWS Management Console authentication attempts.
- Created the custom `FailedConsoleLogins` CloudWatch metric.
- Configured the `SecureCloud-Failed-Console-Login-Alarm` to trigger when a failed console login is detected.
- Configured Amazon SNS email notifications through `SecureCloud-Security-Alerts`.
- Simulated a failed IAM login and successfully received the CloudWatch security alert via email.

### Validation
Successfully verified the end-to-end monitoring pipeline:

CloudTrail → CloudWatch Logs → Metric Filter → CloudWatch Alarm → SNS → Email Alert