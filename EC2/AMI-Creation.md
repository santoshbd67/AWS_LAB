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
