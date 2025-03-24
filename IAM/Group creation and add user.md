# 🔹 Step-by-Step Guide to Create an IAM Group, Add Users, and Assign Permissions (Using AWS Console UI) for POC

## Step 1: Sign in to AWS Management Console

#### Open the AWS Management Console: AWS Console
#### In the search bar, type "IAM" and select IAM from the services list.

## Step 2: Navigate to IAM Groups
#### In the IAM Dashboard, on the left-hand side, click on User Groups.
#### Click the "Create group" button.

## Step 3: Create a New IAM Group
#### Group name: Enter a unique name (e.g., poc-group).
#### Attach Policies to the Group (Select permissions for the group):
#### For Full Admin Access: Attach AdministratorAccess.
#### For EC2 Management: Attach AmazonEC2FullAccess.
#### For S3 Management: Attach AmazonS3FullAccess.
#### For Custom Permissions: Click Create policy (if needed).
#### Click Create group.

## Step 4: Add Users to the Group
#### In the IAM Dashboard, click Users on the left-hand menu.
#### Select the user(s) you want to add to the group.
#### Click "Add to groups".
#### Select the group name (poc-group) created in Step 3.
#### Click Add to group.

## Step 5: Verify Group and User Permissions
#### Go to User Groups in IAM.
#### Click on the newly created group (poc-group).
#### Under the Users tab, verify that the assigned users are listed.
#### Under the Permissions tab, verify that the correct policies are attached.

## ✅ Your IAM group is now created successfully, and users are added! 🎉
