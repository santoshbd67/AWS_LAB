## VPC Overview
#### A VPC (Virtual Private Cloud) is an isolated network in AWS where you can launch your resources securely. It provides full control over IP addressing, routing, and security.

### Key Components & Their Purpose
#### VPC: The main network (e.g., 10.0.0.0/16).
#### Subnets: Smaller networks inside the VPC.
#### Public Subnet: Direct internet access via Internet Gateway (IGW).
#### Private Subnet: No direct internet access; uses NAT Gateway for outbound traffic.
#### Internet Gateway (IGW): Enables internet access for public instances.
#### NAT Gateway: Allows private instances to access the internet securely.
#### Route Tables: Define how traffic flows inside the VPC.
#### Security Groups & NACLs: Act as firewalls to control traffic.

# Step-by-Step Guide
## Step 1: Create VPC
#### VPC Name: MyPOC-VPC

<img width="828" alt="vpcname" src="https://github.com/user-attachments/assets/28a740a8-ee9e-4b3c-a68e-998fbacd694e" />

<img width="890" alt="vpccretae" src="https://github.com/user-attachments/assets/ebb16e7c-6597-4286-9585-48965df003ff" />

#### CIDR Block: 10.0.0.0/16
#### Classless Inter-Domain Routing (CIDR) is an IP address allocation method that improves data routing efficiency on the internet
#### You can use the followinf URL for calculating the CIDR rang
https://www.davidc.net/sites/default/subnets/subnets.html
<img width="541" alt="cidr" src="https://github.com/user-attachments/assets/f1b10d88-6278-4f64-9e9a-c4289063a4a0" />

Step 2: Create Subnets
Public Subnet: 10.0.1.0/24, Enable Auto-assign Public IP
Private Subnet: 10.0.2.0/24, No Public IP
Step 3: Create & Attach Internet Gateway (IGW)
IGW Name: MyIGW
Attach it to MyPOC-VPC.
Step 4: Configure Route Tables
Public Route Table:
Route 0.0.0.0/0 → Internet Gateway
Associate with Public Subnet.
Private Route Table (Later for NAT Gateway).
Step 5: Create NAT Gateway (For Private Subnet Internet Access)
Subnet: Public Subnet
Elastic IP: Allocate & Assign
Step 6: Create Security Groups
Allow SSH (22), HTTP (80), HTTPS (443) for Public Instance.
