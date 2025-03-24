Introduction to AWS Auto Scaling
AWS Auto Scaling is a feature that automatically adjusts the number of EC2 instances in response to demand. It helps maintain application availability and optimize costs by scaling out (adding instances) during high traffic and scaling in (removing instances) when demand decreases.

Key Benefits of Auto Scaling
High Availability – Ensures applications run smoothly without downtime.

Cost Optimization – Automatically removes unnecessary instances, reducing costs.

Fault Tolerance – Replaces failed instances automatically.

Scalability – Adjusts infrastructure to handle fluctuating traffic.

Components of AWS Auto Scaling
Launch Template – Defines EC2 instance settings (AMI, instance type, security group, etc.).

Auto Scaling Group (ASG) – Manages EC2 instances using scaling policies.

Scaling Policies – Defines rules for scaling in and out based on CloudWatch metrics.

CloudWatch Alarms – Monitors metrics (CPU utilization, network traffic, etc.) to trigger scaling events.

Proof of Concept (POC) on AWS Auto Scaling
Step 1: Set Up AWS Environment
Ensure you have an AWS account.

Install AWS CLI (optional but helpful for automation).

Set up IAM roles and permissions to allow Auto Scaling operations.

Step 2: Create a Launch Template
A Launch Template defines how instances will be created when scaling occurs.

Steps to create a Launch Template:
Login to AWS Console → Navigate to EC2.

Click on Launch Templates → Create Launch Template.

Provide a name and description.

Select an Amazon Machine Image (AMI) (e.g., Amazon Linux 2).

Choose an Instance Type (e.g., t2.micro).

Select Key Pair for SSH access.

Configure Networking (VPC, Security Group).

Add User Data (Optional: Can include scripts to configure the instance).

Click Create Launch Template.

Step 3: Create an Auto Scaling Group (ASG)
An ASG maintains the number of instances based on scaling policies.

Steps to create ASG:
Go to EC2 Console → Auto Scaling Groups.

Click Create Auto Scaling Group.

Select the Launch Template created earlier.

Configure Instance Distribution (Choose the number of instances initially).

Select VPC and Subnets (choose public or private subnets as needed).

Set Minimum, Desired, and Maximum instance count.

Configure Scaling Policies:

Target Tracking Scaling: Define CPU Utilization (e.g., 50%).

Step Scaling: Add instances when CPU exceeds a certain threshold.

Scheduled Scaling: Scale at specific times.

Enable Health Checks (EC2 & ELB).

Configure Notifications (Optional).

Click Create Auto Scaling Group.

Step 4: Attach a Load Balancer (Optional)
If you want to distribute traffic evenly, attach an Elastic Load Balancer (ELB).

Steps to attach ELB:
Go to EC2 Console → Load Balancers.

Click Create Load Balancer.

Choose Application Load Balancer (ALB).

Configure Listener (e.g., HTTP/HTTPS).

Choose Target Group and attach it to the Auto Scaling instances.

Link the ASG to the Target Group.

