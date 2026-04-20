## Architecture Explanation

The architecture of this project implements a highly available and secure three-tier web application within a custom-designed Amazon Virtual Private Cloud (VPC). To ensure resilience and fault tolerance, the infrastructure is distributed across two separate Availability Zones, utilizing a mix of public and private subnets to enforce a strict security posture. 

Public-facing traffic enters through an Internet Gateway and is managed by an Application Load Balancer (ALB) residing in the public subnets; this ALB acts as the single entry point, distributing incoming HTTP requests to a fleet of EC2 web servers. These servers are hosted in private subnets, meaning they have no direct exposure to the internet, and are managed by an Auto Scaling Group that automatically adjusts capacity based on demand while performing health checks to replace any failing instances. 

Outbound internet access for these private instances—required for software updates—is facilitated securely through a NAT Gateway. The data layer consists of an Amazon RDS MySQL instance, which is isolated in its own dedicated database subnet group within the private subnets, with security groups configured to allow traffic exclusively from the web server tier. Security is further hardened using IAM Roles with the Principle of Least Privilege, eliminating the need for hardcoded credentials. 

Finally, the entire environment is monitored by a robust CloudWatch suite that tracks system metrics and application logs, with an SNS-integrated alarm system that provides real-time email notifications for critical events such as high CPU utilization, ensuring the infrastructure is not only scalable but also proactively managed.


