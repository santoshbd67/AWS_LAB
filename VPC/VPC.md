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
