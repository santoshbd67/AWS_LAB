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

#### Enter the following details:

#### Host: Paste your RDS Endpoint (e.g., mydb.xxxxxxxx.us-east-1.rds.amazonaws.com).

#### Port: 3306

#### Username: Your RDS username (e.g., admin).

#### Password: Your RDS password.

#### Database: Leave it empty or enter your database name (e.g., mydb).

#### Click Test Connection to verify.

#### Click Connect to access your RDS MySQL database.

## Now you can view and manage your AWS RDS MySQL database from TablePlus on Windows! 🚀
