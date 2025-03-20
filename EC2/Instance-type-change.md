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
