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
  
## Step 3: Create and Attach an Internet Gateway (IGW)
### 💡 IGW allows public subnets to connect to the internet.

### Go to Internet Gateways → Click Create Internet Gateway.
  #### Name: MyIGW → Click Create.
  <img width="953" alt="igw1" src="https://github.com/user-attachments/assets/1c2f911c-2bc4-4ab0-bc31-951b659eb278" />

  <img width="949" alt="igw2" src="https://github.com/user-attachments/assets/9824adae-2f86-4e2d-be60-cada920ff2ad" />

#### Select MyIGW → Click Actions → Attach to VPC.
  #### Select MyPOC-VPC → Click Attach.
<img width="944" alt="igw3" src="https://github.com/user-attachments/assets/81f0716a-fbff-43a5-a996-e5cb98f2f49a" />

<img width="944" alt="igw4" src="https://github.com/user-attachments/assets/3d4986f8-10a1-465e-b5c1-07fb96812ca6" />


## Step 4: Configure Route Tables (RTs)
### 💡 Route Tables define how traffic flows inside the VPC.

### Public Route Table (for Public Subnet)
  #### Go to Route Tables → Click Create Route Table.
#### Name: Public-RT
#### VPC: Select MyPOC-VPC.
#### Click Create.
  <img width="940" alt="rt1" src="https://github.com/user-attachments/assets/5c1aa9ea-6381-4854-b731-c4dd058eb868" />

#### Select Public-RT, go to Routes, and click Edit Routes.
#### Destination: 0.0.0.0/0 (All internet traffic)
#### Target: Select MyIGW
#### Click Save.
<img width="933" alt="edit rt" src="https://github.com/user-attachments/assets/88e67f1d-f312-46c1-a84b-8ad451276ccd" />

<img width="949" alt="editrt1" src="https://github.com/user-attachments/assets/41d42b4d-9ff1-4061-b6f9-7d8866e3256d" />

### Associate it with Public-Subnet:
  #### Click Subnet Associations → Edit Subnet Associations.
  #### Select Public-Subnet → Click Save Associations.
  <img width="938" alt="rt3" src="https://github.com/user-attachments/assets/3a6862a6-c15a-42d1-898d-a56f2a8d3953" />

<img width="944" alt="rt4" src="https://github.com/user-attachments/assets/8dd2924f-a581-44d5-84f9-4cd269f96608" />


### Private Route Table (for Private Subnet)
#### Go to Route Tables → Click Create Route Table.
#### Name: Private-RT
#### VPC: Select MyPOC-VPC.
#### Click Create.

### Associate it with Public-Subnet:
  #### Click Subnet Associations → Edit Subnet Associations.
  #### Select Private-Subnet → Click Save Associations.

## Step 5: Create a NAT Gateway (For Private Subnet Internet Access)
### 💡 NAT Gateway allows private subnet instances to access the internet (for software updates, API calls, etc.) without being exposed.

### Go to NAT Gateways → Click Create NAT Gateway.
  #### Subnet: Choose Public-Subnet.
  #### Elastic IP: Click Allocate New Elastic IP → Click Allocate → Select it.
  #### Click Create NAT Gateway.
  <img width="939" alt="nat1" src="https://github.com/user-attachments/assets/a0743724-6691-4b39-b3a1-1e0a38e9486b" />

  <img width="833" alt="nat2" src="https://github.com/user-attachments/assets/b0485dd6-c079-48fd-b01e-decfcafcb7be" />


  #### Update Private Route Table:
  #### Go to Route Tables → Click Create Route Table.
  #### Name: Private-RT.
  #### VPC: MyPOC-VPC.
  #### Click Create.
  <img width="907" alt="privatert1" src="https://github.com/user-attachments/assets/4388d683-18e7-45f9-b41e-18ebee3165af" />

  #### Select Private-RT → Go to Routes → Edit Routes.
  <img width="932" alt="privatert2" src="https://github.com/user-attachments/assets/1eca2a33-d38c-46a1-b635-fdbbd9438a59" />

  #### Destination: 0.0.0.0/0
  #### Target: Select NAT Gateway
  #### Click Save.
  <img width="947" alt="privatert3" src="https://github.com/user-attachments/assets/ac15c556-b500-4a39-b15f-048321fa36ce" />

  #### Associate it with Private-Subnet:
  #### Click Subnet Associations → Edit Subnet Associations.
  <img width="932" alt="privatert4" src="https://github.com/user-attachments/assets/3f58f3e1-eb2e-4724-8623-d0e1606fecaa" />

  #### Select Private-Subnet → Click Save Associations.
  <img width="938" alt="privatert5" src="https://github.com/user-attachments/assets/7feebf46-4ce5-4a39-b8f7-a0db0a381508" />


