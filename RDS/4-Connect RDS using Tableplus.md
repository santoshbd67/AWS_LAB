# Steps to Download and Connect TablePlus to AWS RDS MySQL on Windows

## Step 1: Download and Install TablePlus

#### Go to the official TablePlus website: https://tableplus.com/

#### Click Download for Windows.

#### Run the downloaded .exe file and follow the installation instructions.


## Step 2: Retrieve AWS RDS MySQL Credentials

#### Open AWS Console → Go to RDS.

#### Click on your MySQL RDS instance.

#### Under Connectivity & Security, copy the Endpoint (e.g., mydb.xxxxxxxx.us-east-1.rds.amazonaws.com).

#### Note the username and password set during RDS creation.

#### Ensure your Security Group allows inbound connections on port 3306 from your Windows IP.


## Step 3: Connect TablePlus to AWS RDS MySQL

#### Open TablePlus.

#### Click Create a New Connection → Select MySQL.
<img width="951" alt="image" src="https://github.com/user-attachments/assets/fcfaeeef-7375-48cb-aef4-651fe859c750" />

#### Enter the following details:

#### Host: Paste your RDS Endpoint (e.g., mydb.xxxxxxxx.us-east-1.rds.amazonaws.com).

#### Port: 3306

#### Username: Your RDS username (e.g., admin).

#### Password: Your RDS password.

#### Database: Leave it empty or enter your database name (e.g., mydb).

#### Click Test Connection to verify.

#### Click Connect to access your RDS MySQL database.
<img width="924" alt="image" src="https://github.com/user-attachments/assets/05466bde-8728-45ad-a1d8-6a5a7baa2f82" />

<img width="952" alt="image" src="https://github.com/user-attachments/assets/6d1aa87b-57dd-4baa-9349-09d736ce41d8" />

## Note: To connect to TablePlus, we need to modify the RDS security group by adding the public IP of our laptop and setting the RDS instance to public access. However, this is not recommended for production due to security risks.

## Now you can view and manage your AWS RDS MySQL database from TablePlus on Windows! 🚀
