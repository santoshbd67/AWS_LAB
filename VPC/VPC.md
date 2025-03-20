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

# Step-by-Step Guide For Creation of VPC 
## Step 1: Create VPC
#### VPC Name: MyPOC-VPC

<img width="828" alt="vpcname" src="https://github.com/user-attachments/assets/28a740a8-ee9e-4b3c-a68e-998fbacd694e" />

#### CIDR Block: 10.0.0.0/16
#### Classless Inter-Domain Routing (CIDR) is an IP address allocation method that improves data routing efficiency on the internet
#### You can use the followinf URL for calculating the CIDR rang
#### https://www.davidc.net/sites/default/subnets/subnets.html
<img width="541" alt="cidr" src="https://github.com/user-attachments/assets/f1b10d88-6278-4f64-9e9a-c4289063a4a0" />
<img width="890" alt="vpccretae" src="https://github.com/user-attachments/assets/ebb16e7c-6597-4286-9585-48965df003ff" />

## Step 2: Create Subnets
### 💡 Subnets divide the VPC into smaller sections for better resource management.

#### Go to Subnets → Click Create Subnet.
  #### Select VPC: MyPOC-VPC.
  #### Create Public Subnet
  #### Name: Public-Subnet
  #### CIDR: 10.0.0.0/19 (256 IPs)
  #### Availability Zone: Choose of your choice
  #### Auto-assign public IPv4: Enable
  #### Click Create Subnet.

<img width="715" alt="subnet1" src="https://github.com/user-attachments/assets/3d45141f-97a1-457a-87a4-222d630063a3" />

<img width="760" alt="subnet2" src="https://github.com/user-attachments/assets/4ab34248-9fc2-475f-b2fc-33fa602a3089" />

<img width="943" alt="subnet3" src="https://github.com/user-attachments/assets/00310a59-f5be-4263-a5f5-a071bde4f086" />

 ### Same way create private subnet
  #### Create Private Subnet
  #### Name: Private-Subnet
  #### CIDR: 10.0.32.0/19
  ####  Availability Zone: Same or different from the public subnet
  #### Auto-assign public IPv4: Disable
  #### Click Create Subnet.
  
Step 3: Create and Attach an Internet Gateway (IGW)
💡 IGW allows public subnets to connect to the internet.

Go to Internet Gateways → Click Create Internet Gateway.
Name: MyIGW → Click Create.
Select MyIGW → Click Actions → Attach to VPC.
Select MyPOC-VPC → Click Attach.
Step 4: Configure Route Tables (RTs)
💡 Route Tables define how traffic flows inside the VPC.

Public Route Table (for Public Subnet)
Go to Route Tables → Click Create Route Table.
Name: Public-RT
VPC: Select MyPOC-VPC.
Click Create.
Select Public-RT, go to Routes, and click Edit Routes.
Destination: 0.0.0.0/0 (All internet traffic)
Target: Select MyIGW
Click Save.
Associate it with Public-Subnet:
Click Subnet Associations → Edit Subnet Associations.
Select Public-Subnet → Click Save Associations.
Step 5: Create a NAT Gateway (For Private Subnet Internet Access)
💡 NAT Gateway allows private subnet instances to access the internet (for software updates, API calls, etc.) without being exposed.

Go to NAT Gateways → Click Create NAT Gateway.
Subnet: Choose Public-Subnet.
Elastic IP: Click Allocate New Elastic IP → Click Allocate → Select it.
Click Create NAT Gateway.
Update Private Route Table:
Go to Route Tables → Click Create Route Table.
Name: Private-RT.
VPC: MyPOC-VPC.
Click Create.
Select Private-RT → Go to Routes → Edit Routes.
Destination: 0.0.0.0/0
Target: Select NAT Gateway
Click Save.
Associate it with Private-Subnet:
Click Subnet Associations → Edit Subnet Associations.
Select Private-Subnet → Click Save Associations.

