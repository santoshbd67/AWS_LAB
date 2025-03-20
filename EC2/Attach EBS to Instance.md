## Steps to Attach a New EBS Volume to an EC2 Instance
  ### Amazon Elastic Block Store (EBS) provides scalable storage that can be attached to EC2 instances for additional space. This guide will walk you through creating, attaching, and mounting a new EBS volume on an existing EC2 instance.

### Step 1: Create a New EBS Volume
  #### Log in to the AWS Console → Go to EC2 Dashboard.
  #### In the left panel, click Volumes (under Elastic Block Store).
#### Click Create Volume.
#### Configure the volume:
#### Size: Enter required size (e.g., 10 GiB).
#### Volume Type: Choose gp3 (General Purpose SSD).
#### Availability Zone (AZ): Must match your EC2 instance's AZ.
#### Example: If the instance is in us-east-1a, the EBS must be in us-east-1a.
#### Encryption: Choose if needed.
#### Click Create Volume.

### Step 2: Attach the EBS Volume to the EC2 Instance
#### In the Volumes section, find your newly created volume.
#### Select the volume → Click Actions → Attach Volume.
#### Choose:
#### Instance: Select your running EC2 instance.
#### Device Name: Default is /dev/xvdf (for Linux).
#### Click Attach Volume.

### Step 3: Connect to Your EC2 Instance
#### Copy your Public IP from EC2 Dashboard.
#### Connect via SSH:
```
ssh -i my-key.pem ubuntu@<public-ip>
```
List available block devices to verify attachment:
```
lsblk
```
#### You should see an unmounted volume (e.g., /dev/xvdf).

### Step 4: Format and Mount the EBS Volume
#### Check if the volume has a filesystem (it will show data if formatted):
```
sudo file -s /dev/xvdf
```
#### If it returns data, the volume is not formatted.
### Format the volume (Only if it's new & unformatted):
```
sudo mkfs -t ext4 /dev/xvdf
```
#### Create a mount point (Example: /mnt/newvolume):
```
sudo mkdir /mnt/newvolume
```

#### Mount the EBS Volume:
```
sudo mount /dev/xvdf /mnt/newvolume
```
#### Verify the mount:
```
df -h
```
#### You should see /mnt/newvolume in the list.


