##  Launch an EC2 Instance
#### Log in to AWS Console
##### Open AWS Console and log in.
##### Search for EC2 in the top search bar and select EC2 Dashboard.

<img width="787" alt="ec2 search" src="https://github.com/user-attachments/assets/6bef0794-6a6d-498c-a6df-730c28de6519" />

####  Create a New EC2 Instance
##### Click Launch instance.
<img width="943" alt="launch" src="https://github.com/user-attachments/assets/5bb0f8f0-9d6b-4030-8fea-e0a992c16f80" />

##### Enter a Name for your instance (e.g., MyEC2Instance).
<img width="634" alt="name" src="https://github.com/user-attachments/assets/20cfac45-451a-43dd-b786-faf35c59fecd" />

##### Choose an Amazon Machine Image (AMI) (e.g., Amazon Linux 2 or Ubuntu).
<img width="595" alt="ami" src="https://github.com/user-attachments/assets/075bbed4-838e-476c-b516-b3285fc75ff7" />

##### Select an Instance Type (e.g., t2.micro).
##### Configure Key Pair for SSH access or create a new one.
<img width="629" alt="instance type" src="https://github.com/user-attachments/assets/381f8b30-8a4f-4cff-8422-469a54fcb310" />

<img width="715" alt="keypair" src="https://github.com/user-attachments/assets/a8f0ff35-dc28-4911-8861-05dc1ffe6d66" />


##### Under Network Settings, ensure a Security Group allows SSH (port 22) and other necessary ports (80, 443, etc.).
<img width="617" alt="sg" src="https://github.com/user-attachments/assets/a32dc2d0-9523-4067-a0a1-a563d718dea7" />

##### Under Storage Configuration, you’ll see a Root EBS Volume attached.
##### Default size is 8 GiB (you can increase it here or modify it later).
<img width="623" alt="ebs" src="https://github.com/user-attachments/assets/f9c03ed9-e540-459f-b59c-12c31058e32f" />

##### Click Launch instance.
<img width="932" alt="image" src="https://github.com/user-attachments/assets/5dd4185e-ceff-4aec-96f8-9026bd25ba56" />

##### Wait for the instance to launch, then navigate to Instances and confirm its status is Running.
<img width="954" alt="running" src="https://github.com/user-attachments/assets/b8c9cafd-7f67-4a74-ae17-ee265f16029f" />



## Change the EC2 Instance Type Using AWS Management Console (UI)
#### After modifying the EBS volume size and extending the file system, you may need to upgrade or downgrade the EC2 instance type based on performance needs. Follow these steps

##  Change the EC2 Instance Type
####  Stop the EC2 Instance
#### Log in to AWS Console and go to EC2 Dashboard.
#### Click Instances in the left panel.
#### Select the instance whose type you want to change.
#### Click Instance State → Stop Instance → Confirm.
<img width="913" alt="type" src="https://github.com/user-attachments/assets/44927e8e-bc91-48a2-87c9-def03c0ccfc7" />

#### ⚠️ Stopping the instance is required before changing the instance type.

####  Modify the Instance Type
#### Select the stopped instance.
#### Click Actions → Instance Settings → Change Instance Type.
<img width="941" alt="instancetyoe" src="https://github.com/user-attachments/assets/347f0a37-a48d-436a-97c6-9d9a16d4c7b5" />

#### Choose the new Instance Type (e.g., change from t2.micro to t2.medium).
#### Click Apply to save changes.
#### Start the EC2 Instance
#### Click Instance State → Start Instance.
#### Wait for the instance status to change to Running.
