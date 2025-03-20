## Steps to Copy an AMI in AWS
### Copying an Amazon Machine Image (AMI) allows you to move an AMI between AWS regions or within the same region for redundancy, backups, or scaling.

### Step 1: Open the AWS EC2 Dashboard
#### Log in to the AWS Console.
#### Navigate to EC2 → Click AMIs from the left panel.
#### Find the AMI you want to copy.
#### Select the AMI → Click Actions → Copy AMI.

### Step 2: Configure the AMI Copy Settings
#### Destination Region: Select the region where you want to copy the AMI.
#### New AMI Name: Provide a name (e.g., MyCopiedAMI).
#### Description (Optional): Add a short description.
#### Encryption:
#### If the source AMI is encrypted, you must copy it with encryption.
#### If the source AMI is not encrypted, you can choose to encrypt it.
#### Click Copy AMI.
<img width="952" alt="copyami1" src="https://github.com/user-attachments/assets/799f91e6-bed6-4413-847e-cf06598a077a" />

<img width="635" alt="copyami2" src="https://github.com/user-attachments/assets/ac077c26-c559-4856-b689-6330de453c30" />

