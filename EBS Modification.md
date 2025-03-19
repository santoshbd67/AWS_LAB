## Locate the EBS Volume
#### In the EC2 Dashboard, go to the left panel and select Volumes under Elastic Block Store (EBS).
#### Locate the volume attached to your EC2 instance:
#### Check the Attachment Information column.
#### You can also check Instance ID under the EC2 > Instances > Storage tab.
<img width="950" alt="volume" src="https://github.com/user-attachments/assets/98e884bf-0891-4d9b-b9b9-e72c39802dc1" />


##  Modify the EBS Volume Size
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

#### Connect to Your EC2 Instance via SSH
#### Open a terminal and run:
```
ssh -i your-key.pem ec2-user@your-instance-ip
```
#### (Replace your-key.pem with your private key file and your-instance-ip with the public IP of your EC2 instance.)
####  Check the Current Disk Size
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

####  Extend the Partition (If Needed)
#### If your partition does not automatically expand:
```
sudo growpart /dev/xvda 1
```
####  Resize the File System
#### For ext4 file system (Amazon Linux 2, Ubuntu):
```
sudo resize2fs /dev/xvda1
```
#### For XFS file system (Amazon Linux 2, RHEL):
```
sudo xfs_growfs /
```
#### Verify the Changes
#### Run the command again:
```
df -h
```
#### You should see the updated file system reflecting the new size.
