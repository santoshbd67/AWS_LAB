## Step 1: Launch an EC2 Instance
#### 1.1 Log in to AWS Console
##### Open AWS Console and log in.
##### Search for EC2 in the top search bar and select EC2 Dashboard.

<img width="787" alt="ec2 search" src="https://github.com/user-attachments/assets/6bef0794-6a6d-498c-a6df-730c28de6519" />

#### 1.2 Create a New EC2 Instance
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

## Step 2: Locate the EBS Volume
#### In the EC2 Dashboard, go to the left panel and select Volumes under Elastic Block Store (EBS).
#### Locate the volume attached to your EC2 instance:
#### Check the Attachment Information column.
#### You can also check Instance ID under the EC2 > Instances > Storage tab.
<img width="950" alt="volume" src="https://github.com/user-attachments/assets/98e884bf-0891-4d9b-b9b9-e72c39802dc1" />


## Step 3: Modify the EBS Volume Size
#### In the EBS Volumes section, select the attached volume.
#### Click Actions → Modify Volume.
<img width="949" alt="modify" src="https://github.com/user-attachments/assets/c30edad9-e91c-4cb3-a591-7b714fe2a5c0" />

#### In the Modify Volume dialog box:
#### Increase the Size (GiB) (e.g., from 8 GiB to 30 GiB).
#### Keep the Volume Type unchanged (unless necessary).
#### Click Modify and confirm.
<img width="938" alt="changed" src="https://github.com/user-attachments/assets/066ec4a5-6aea-4832-895e-9b587be2fab2" />

#### AWS will now resize the volume, but you need to update the OS to use the additional space.

## Step 4: Extend the File System on EC2 (Linux Instance)
#### After increasing the volume, you must extend the file system on your EC2 instance.

#### 4.1 Connect to Your EC2 Instance via SSH
#### Open a terminal and run:
```
ssh -i your-key.pem ec2-user@your-instance-ip
```
#### (Replace your-key.pem with your private key file and your-instance-ip with the public IP of your EC2 instance.)
#### 4.2 Check the Current Disk Size
Run the following command to check the available disk space:
```
lsblk
```
#### It will show something like:
```
NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
xvda    202:0    0  30G  0 disk
└─xvda1 202:1    0  8G   0 part /
Here, xvda is the full 30 GiB disk, but the partition xvda1 is still 8 GiB.
```

#### 4.3 Extend the Partition (If Needed)
#### If your partition does not automatically expand:
```
sudo growpart /dev/xvda 1
```
#### 4.4 Resize the File System
#### For ext4 file system (Amazon Linux 2, Ubuntu):
```
sudo resize2fs /dev/xvda1
```
#### For XFS file system (Amazon Linux 2, RHEL):
```
sudo xfs_growfs /
```
#### 4.5 Verify the Changes
#### Run the command again:
```
df -h
```
#### You should see the updated file system reflecting the new size.
