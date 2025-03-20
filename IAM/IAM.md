## AWS Identity and Access Management (IAM) - Detailed Explanation
#### AWS Identity and Access Management (IAM) is a service that allows you to manage who can access AWS resources and what they can do with them.

#### IAM helps in securing your AWS environment by controlling access without using passwords or keys in many cases.

### Key Components of IAM
  #### 1. IAM Users 👤
  #### An IAM User represents an individual who needs access to AWS resources.

  #### * Each user has a username, password, and access keys (for programmatic access).
#### * Permissions are assigned using IAM Policies.
#### * Example: A developer with permission to access EC2 but not S3.

#### ✅ Use Case: Create an IAM user for each employee instead of using the root user.

### 2. IAM Groups 📂
#### An IAM Group is a collection of users with similar permissions.

#### *Instead of assigning permissions to users individually, you assign them to a group.
#### * Example:
  #### 1 Admin Group → Full access to AWS.
  #### 2 Developers Group → Access to EC2 & S3 but not IAM.
  
#### ✅ Use Case: Easily manage permissions for multiple users at once.


### 3. IAM Policies 📜
#### IAM Policies are JSON documents that define permissions.

#### * They are attached to users, groups, or roles to grant or deny access.
#### * Example of a policy that allows read-only access to S3:
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::my-bucket"
    }
  ]
}
```

#### ✅ Use Case: Restrict access to only required AWS services.

### 4. IAM Roles 🎭
#### IAM Roles allow AWS services or users to assume temporary permissions.

#### * Unlike IAM Users, roles do not require passwords or access keys.
#### * AWS services (like EC2, Lambda, or S3) assume IAM roles to perform actions.
#### * Example:
#### 1 EC2 Role with S3 access → Lets an EC2 instance upload files to S3 without hardcoded credentials.

#### ✅ Use Case: Secure service-to-service communication without exposing credentials.



