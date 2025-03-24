# 🔹 Step-by-Step Guide to Create an IAM User Using AWS Console (UI) for POC

## Step 1: Sign in to AWS Management Console

#### Open the AWS Management Console: AWS Console
#### In the top-right corner, click on your account name and select "IAM" from the dropdown.
#### Alternatively, search for "IAM" in the AWS services search bar and click on "IAM".

## Step 2: Navigate to IAM Users

#### In the IAM Dashboard, on the left-hand menu, click Users.
#### Click the “Add users” button.

## Step 3: Provide User Details

#### User name: Enter a unique user name (e.g., poc-user).
#### Access Type:
#### If the user needs AWS Management Console access, check “Provide user access to the AWS Management Console” and set an initial password.
#### If the user needs programmatic access (CLI, SDK, API), check "Provide access key – Programmatic access".
#### You can enable both options if needed.
#### Click Next.

## Step 4: Set Permissions for the User

### You can assign permissions in three ways:

### Option 1: Attach Policies Directly (Recommended for POC)
#### In the Set Permissions step, select “Attach policies directly”.
#### Use the search bar to find a relevant policy:
#### For Admin Access, select AdministratorAccess.
#### For EC2 Access, select AmazonEC2FullAccess.
#### For S3 Access, select AmazonS3FullAccess.
#### For Custom Access, choose the required policy or create a new one.
#### Click Next.

### Option 2: Add User to a Group
#### Select "Add user to group".
#### Click "Create group", enter a group name (e.g., poc-group).
#### Attach required permissions (e.g., AdministratorAccess or AmazonS3FullAccess).
#### Click Create group, then select the created group.
#### Option 3: Copy Permissions from an Existing User
#### Select “Copy permissions from existing user”.
#### Choose an IAM user with similar permissions.
#### Click Next.

33 Step 5: Review & Create User

#### Review the user details, permissions, and access types.
#### Click Create user.

## Step 6: Download Credentials

#### If programmatic access was enabled, download the Access Key ID and Secret Access Key by clicking "Download .csv".
#### Save this file securely, as AWS will not show the secret key again.
#### Click Close.

## Step 8: Verify User Login (If Console Access was Enabled)

#### Go to the IAM Dashboard → Users.
#### Click on the new user.
#### Under "Security credentials", copy the Sign-in URL (e.g., https://123456789012.signin.aws.amazon.com/console).
#### Open the URL and log in with:
#### Username: The IAM user name.
#### Password: The one set during creation (or provided via email if "Auto-generate" was selected).

### ✅ Your IAM user is now created successfully! 🎉

