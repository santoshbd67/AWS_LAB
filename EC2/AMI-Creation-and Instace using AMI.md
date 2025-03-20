## What is an AMI?
#### An Amazon Machine Image (AMI) is a pre-configured template used to launch EC2 instances. It includes:
#### ✅ Operating System (Ubuntu, Amazon Linux, Windows, etc.)
#### ✅ Pre-installed Software & Configurations
#### ✅ System Settings & Customizations

### Use Cases of AMIs
#### ✔ Faster Instance Deployment – Pre-configured instances launch quickly.
#### ✔ Disaster Recovery – Take backups and restore servers easily.
#### ✔ Auto Scaling – Use AMIs for launching identical instances in Auto Scaling Groups.

## Step-by-Step Guide to Create and Use an AMI

### Step 1: Select an Existing EC2 Instance
  #### Log in to AWS Console → Go to EC2 Dashboard.
  #### Click Instances from the left panel.
  #### Select the instance you want to create an AMI from.
### Step 2: Create an AMI
  #### Click Actions → Image and Templates → Create Image.
  #### Fill in the details:
  #### Image Name: MyCustomAMI
  #### Description: AMI with pre-installed software
  #### No Reboot (Optional):
  #### Checked: Instance won't reboot (may cause issues).
  #### Unchecked: AWS reboots the instance for a clean image.
  #### Click Create Image.
  <img width="938" alt="amicreate1" src="https://github.com/user-attachments/assets/e8cc713c-531a-4381-8856-d0c597c45088" />

  <img width="869" alt="amifinal" src="https://github.com/user-attachments/assets/29b5fe4e-936c-4dec-bfdf-c2b2158692f3" />


  ## Steps to Launch an EC2 Instance Using an Existing AMI
  #### Now that you have created an AMI, follow these steps to launch a new EC2 instance using that AMI.

### Step 1: Open the AWS EC2 Dashboard
  #### Log in to AWS Console → Navigate to EC2 Dashboard.
  #### In the left panel, click on AMIs (under "Images").
  #### Find and select your AMI (e.g., MyCustomAMI).

### Step 2: Launch an Instance from the AMI
  #### Select MyCustomAMI.
  #### Click Launch Instance from Image.
  #### Choose Instance Type (e.g., t2.micro for free-tier).
  #### Configure Instance Details:
  #### Network (VPC): Select your existing VPC.
  #### Subnet: Choose a public or private subnet.
  #### Auto-assign Public IP: Enable for internet access.
  
### Step 3: Configure Storage
  #### Keep the default volume size or modify it as needed.
  #### Click Next to add optional tags (e.g., Key: Name, Value: MyAMIInstance).
  
### Step 4: Configure Security Group
  #### Select an existing Security Group or create a new one.
  #### Ensure necessary rules are added (e.g., allow SSH, HTTP, HTTPS).
  
### Step 5: Select Key Pair & Launch the Instance
  #### Choose an existing key pair or create a new one.
  #### Check the box I acknowledge... if creating a new key.
#### Click Launch Instance.

  <img width="925" alt="launchami1" src="https://github.com/user-attachments/assets/77ca9fe6-6ddd-4fb3-8b10-662bf109242a" />

<img width="939" alt="launchami2" src="https://github.com/user-attachments/assets/19f68412-04e1-4bb3-98ea-979bb0a45edf" />

<img width="906" alt="launchami3" src="https://github.com/user-attachments/assets/1c3856df-a492-4f90-8cf7-8795bb47dcc6" />



