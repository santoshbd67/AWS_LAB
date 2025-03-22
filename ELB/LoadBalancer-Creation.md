### What is a Load Balancer?
A Load Balancer is a networking service that distributes incoming traffic across multiple targets (such as EC2 instances, containers, or IP addresses) to ensure high availability and fault tolerance.

#### Types of Load Balancers in AWS
#### AWS provides different types of Elastic Load Balancers (ELB):

### Application Load Balancer (ALB) – Best for HTTP/HTTPS traffic (Layer 7)
### Network Load Balancer (NLB) – Best for ultra-low latency (Layer 4)
### Classic Load Balancer (CLB) – Legacy version
#### For this POC, we will create an Application Load Balancer (ALB) with a Target Group that routes traffic to EC2 instances.

## Steps to Create Load Balancer and Target Group (Using AWS UI)
### Step 1: Create a Target Group
#### A Target Group defines how the load balancer routes requests to backend instances.

### 1.1 Navigate to Target Groups
#### In the EC2 Dashboard, scroll down to Load Balancing.
#### Click on Target Groups (left-hand menu).
#### Click Create Target Group.
<img width="945" alt="image" src="https://github.com/user-attachments/assets/aaa51e7f-db0c-4089-8917-3c25737ae19d" />

### 1.2 Configure the Target Group
#### Choose Target Type:
#### Select Instances (for EC2-based apps) or IP addresses (for external apps).
<img width="794" alt="image" src="https://github.com/user-attachments/assets/f5502b5a-ae09-4b76-9c15-2f937cae7442" />

#### Enter a Name:
#### Example: my-target-group.
#### Protocol and Port:
#### Select HTTP or HTTPS.
#### Set Port (e.g., 80 for HTTP or 443 for HTTPS).
#### VPC Selection:
#### Choose the VPC where your EC2 instances are running.
#### Health Checks:
#### Protocol: HTTP
<img width="944" alt="image" src="https://github.com/user-attachments/assets/52263504-a128-4a92-bab2-fc95c3f4bfb4" />

#### Path: / (or /health if your app has a health check endpoint).
#### Click Next.
### 1.3 Register Targets (EC2 Instances)
#### Select your running EC2 instances.
#### Click Include as pending below.
#### Click Create target group.
<img width="949" alt="image" src="https://github.com/user-attachments/assets/54bb89bf-7ea0-4959-b035-08e9242f2a67" />

#### ✅ Target Group Created!

## Step 2: Create an Application Load Balancer (ALB)

### 2.1 Navigate to Load Balancers
#### In the EC2 Dashboard, go to Load Balancers (under Load Balancing).
#### Click Create Load Balancer.
#### Choose Application Load Balancer (ALB) and click Create.
<img width="897" alt="image" src="https://github.com/user-attachments/assets/d8d889bf-b133-4cef-8527-561f2a0fb8f7" />

### 2.2 Configure Load Balancer
#### Name: Example → my-load-balancer.
#### Scheme:
#### Internet-facing (for public access)
#### Internal (for internal network only)
#### IP Address Type: IPv4
<img width="679" alt="image" src="https://github.com/user-attachments/assets/2609dbec-0346-4a28-88a4-8bc1f422c59f" />

#### Listeners:
#### Add HTTP (port 80) or HTTPS (port 443) (if using SSL).

#### VPC and Availability Zones:
#### Select your VPC and at least two availability zones.
### 2.3 Configure Security Group
#### Select an existing security group or create a new one:
#### Allow inbound traffic on ports 80 (HTTP) and 443 (HTTPS).
### 2.4 Configure Routing
#### Select the Target Group you created earlier (my-target-group).
#### Keep the Protocol as HTTP (or HTTPS if SSL is enabled).
<img width="688" alt="image" src="https://github.com/user-attachments/assets/8c79dbe4-9935-428c-aa7c-c069ea339556" />

#### Click Next: Register Targets.
### 2.5 Review and Create
#### Review all settings.
#### Click Create Load Balancer.
<img width="922" alt="image" src="https://github.com/user-attachments/assets/32deac84-23b6-4eb6-95c9-b96cac738d1d" />

#### Wait a few minutes until the status changes to Active.
#### ✅ Load Balancer Created!

## Step 3: Verify Load Balancer
#### Go to Load Balancers in the AWS EC2 dashboard.
#### Copy the DNS name of the Load Balancer.
#### Paste it into your browser (http://your-load-balancer-dns-name).
#### If everything is set up correctly, you should see your application running!
