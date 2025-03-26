# Step-by-Step Guide to Creating an RDS Instance in AWS

## Step 1: Log in to AWS Console
#### Go to the AWS Management Console: https://aws.amazon.com/console/
#### In the Search Bar, type RDS and click on Amazon RDS.

## Step 2: Create a New RDS Database
#### Click on Create database.
<img width="952" alt="image" src="https://github.com/user-attachments/assets/a71ae866-a60b-4a3c-a10c-b3c125eecf00" />

#### Under Choose a database creation method, select Standard Create.
#### Under Engine options, select the database engine:

#### MySQL

#### PostgreSQL

#### MariaDB

#### Oracle

#### SQL Server

#### Amazon Aurora
<img width="928" alt="image" src="https://github.com/user-attachments/assets/98076e0e-5998-4ee2-aafe-8fa6eb6bfd26" />


#### Select Database version (e.g., MySQL 8.0, PostgreSQL 14).
<img width="895" alt="image" src="https://github.com/user-attachments/assets/ce082db9-d104-42ac-a7c6-18ce42c5408c" />


## Step 3: Configure Database Settings
#### DB instance identifier – Give a unique name (e.g., my-rds-db).
#### Credentials Settings:
#### Master username: admin (or any preferred username)
#### Password: Set a strong password and confirm.
<img width="932" alt="image" src="https://github.com/user-attachments/assets/1c56b8ee-0437-493a-8c5a-2fe8b7f166c7" />

## Step 4: Select Instance Type & Storage

#### DB Instance Class:
#### For Free Tier, choose db.t3.micro (1 vCPU, 1GB RAM).
#### For production, choose db.m5.large or higher.
#### Storage:
#### Allocated storage: Set to 20GB (for Free Tier) or higher as needed.
#### Enable Storage autoscaling (recommended).
<img width="949" alt="image" src="https://github.com/user-attachments/assets/3ef8a1bf-d4d7-4ce9-9f58-b51ae6201d69" />


## Step 5: Configure Networking & Security

#### VPC – Choose the existing VPC or create a new one.
#### Subnet Group – Use the default subnet group for Multi-AZ availability.
#### Public Access –
#### Yes (if accessing from outside AWS, e.g., your local machine).
#### No (if accessing from an EC2 instance inside the VPC).
<img width="949" alt="image" src="https://github.com/user-attachments/assets/cdb1fab9-ca9a-4f8c-be77-18492292bff2" />

#### Security Group:
#### Create a new security group.
#### Allow inbound 3306 (MySQL), 5432 (PostgreSQL), etc.
#### Source: Select My IP if connecting from your laptop.

## Step 6: Additional Configurations

#### Database Authentication:
#### Select Password authentication (for standard login).
#### Backup:
#### Enable Automated backups (choose retention period 7 days or more).
<img width="773" alt="image" src="https://github.com/user-attachments/assets/01966504-1ce3-413a-a0d5-18d7e8c5ec4d" />

#### Monitoring:
#### Enable Enhanced Monitoring for real-time database performance metrics.
#### Maintenance:
#### Choose a maintenance window for automatic updates.
#### Performance Insights:
#### Enable Performance Insights (recommended for debugging slow queries).

## Step 7: Review and Create

#### Double-check your configurations.
#### Click Create Database.
#### Wait for the database to be in the Available state (may take a few minutes).
<img width="780" alt="image" src="https://github.com/user-attachments/assets/5a1feb52-0b91-4f83-9e48-7672558c8094" />

