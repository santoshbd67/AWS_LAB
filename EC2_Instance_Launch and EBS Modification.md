## Step 1: Launch an EC2 Instance
#### 1.1 Log in to AWS Console
##### Open AWS Console and log in.
##### Search for EC2 in the top search bar and select EC2 Dashboard.

<img width="787" alt="ec2 search" src="https://github.com/user-attachments/assets/6bef0794-6a6d-498c-a6df-730c28de6519" />

#### 1.2 Create a New EC2 Instance
##### Click Launch instance.
##### Enter a Name for your instance (e.g., MyEC2Instance).
##### Choose an Amazon Machine Image (AMI) (e.g., Amazon Linux 2 or Ubuntu).
##### ##### Select an Instance Type (e.g., t2.micro).
##### Configure Key Pair for SSH access or create a new one.
##### Under Network Settings, ensure a Security Group allows SSH (port 22) and other necessary ports (80, 443, etc.).
##### Under Storage Configuration, you’ll see a Root EBS Volume attached.
##### Default size is 8 GiB (you can increase it here or modify it later).
##### Click Launch instance.
##### Wait for the instance to launch, then navigate to Instances and confirm its status is Running.
