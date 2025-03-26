# Steps to Connect MySQL RDS from an Ubuntu EC2 Instance

## Step 1: Launch an EC2 Instance (Ubuntu)

#### Open AWS Console → Go to EC2.

#### Click Launch Instance.

#### Choose Ubuntu as the AMI.
<img width="920" alt="image" src="https://github.com/user-attachments/assets/fc99fac7-60f4-4e96-98a7-a05722ed31d3" />

#### Select Instance Type (e.g., t2.micro for Free Tier).
<img width="760" alt="image" src="https://github.com/user-attachments/assets/e7d625eb-6cc3-4917-b3a5-c3016be97561" />

#### In Network Settings:

#### Ensure EC2 is in the same VPC as the RDS instance.
<img width="599" alt="image" src="https://github.com/user-attachments/assets/a1101e6f-09b4-49df-9d1a-b8ad142a090e" />

#### Choose or create a Security Group.

#### Click Launch and wait for the instance to be running.


## Step 2: Configure RDS Security Group to Allow EC2 Access

#### Go to AWS Console → EC2 → Security Groups.

#### Select the Security Group attached to your RDS instance.
<img width="922" alt="image" src="https://github.com/user-attachments/assets/0acbbc31-8a87-4330-8058-c5e4c9fa415c" />

#### Click Inbound Rules → Edit Inbound Rules → Add Rule:
<img width="946" alt="image" src="https://github.com/user-attachments/assets/2e2f1778-34d9-4c18-ac63-9be0f8e9a597" />

#### Type: MySQL/Aurora.

#### Protocol: TCP.

#### Port: 3306.

#### Source: Select EC2 Security Group (not "My IP").

#### Save the changes.
<img width="944" alt="image" src="https://github.com/user-attachments/assets/11c88894-186a-4905-bf55-8a66b83f15bd" />


## Step 3: Connect to EC2 via SSH

#### From your local system, connect to the EC2 instance using SSH:
```
ssh -i /path/to/your-key.pem ubuntu@your-ec2-public-ip
```
#### Replace:
#### /path/to/your-key.pem with your actual key file path.
#### your-ec2-public-ip with the public IP of your EC2 instance.

## Step 4: Install MySQL Client on EC2

#### On the EC2 instance, update the system and install MySQL client:
```
sudo apt update
sudo apt install mysql-client -y
```

## Step 5: Retrieve RDS Endpoint

#### Go to AWS Console → RDS.

#### Click on your RDS instance.

#### Copy the "Endpoint" under Connectivity & Security.

#### Example endpoint:
```
my-rds-instance.xxxxxx.us-east-1.rds.amazonaws.com
```

## Step 6: Connect to MySQL RDS from EC2

#### Run the following command:
```
mysql -h my-rds-instance.xxxxxx.us-east-1.rds.amazonaws.com -P 3306 -u admin -p
```
#### Replace my-rds-instance.xxxxxx.us-east-1.rds.amazonaws.com with your RDS endpoint.

#### Enter your RDS password when prompted.

## Step 7: Verify Connection

#### Once connected, run:
```
SHOW DATABASES;
```
#### If successful, you should see a list of databases.

## Step 8: Basic SQL Commands

#### Create a new database:
```
CREATE DATABASE mydb;
```
#### Use the database:
```
USE mydb;
```
#### Create a table:
```
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
#### Insert data:
```
INSERT INTO users (name, email) VALUES ('John Doe', 'john@example.com');
```
#### Retrieve data:
```
SELECT * FROM users;
```

## Step 9: Troubleshooting

#### Access denied?

#### Ensure you are using the correct username and password.

#### Check if RDS Security Group allows EC2's Security Group.

#### Can't connect?

#### Check if RDS is "Publicly Accessible" (for external access).

#### Run telnet to test connectivity:
```
telnet my-rds-instance.xxxxxx.us-east-1.rds.amazonaws.com 3306
```
