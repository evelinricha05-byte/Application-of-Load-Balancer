# AWS Application Load Balancer (ALB) Setup

## Overview
This repository provides instructions to set up an **Application Load Balancer (ALB)** in AWS to distribute HTTP/HTTPS traffic across multiple EC2 instances.

---

## Architecture
- **VPC** with public subnets in at least 2 availability zones
- **Internet Gateway** attached to VPC
- **EC2 instances** running the web application
- **Target Group** with EC2 instances
- **Application Load Balancer**
- **Security Groups** allowing HTTP/HTTPS traffic

---

## Prerequisites
- AWS account
- AWS CLI configured (optional)
- Running EC2 instances
- Basic knowledge of VPC and networking

---

## Steps to Set Up ALB

### 1. Create a Target Group
```bash
aws elbv2 create-target-group \
    --name my-targets \
    --protocol HTTP \
    --port 80 \
    --vpc-id <your-vpc-id> \
    --target-type instance
aws elbv2 register-targets \
    --target-group-arn <target-group-arn> \
    --targets Id=<instance-id-1> Id=<instance-id-2>
aws elbv2 create-load-balancer \
    --name my-alb \
    --subnets <subnet-1> <subnet-2> \
    --security-groups <security-group-id> \
    --scheme internet-facing \
    --type application
aws elbv2 create-listener \
    --load-balancer-arn <alb-arn> \
    --protocol HTTP \
    --port 80 \
    --default-actions Type=forward,TargetGroupArn=<target-group-arn>



