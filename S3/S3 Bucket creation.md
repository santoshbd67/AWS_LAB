# 🔹 Step-by-Step Guide to Create an S3 Bucket and Upload a File (Using AWS Console UI) for POC

## Step 1: Sign in to AWS Management Console
#### Open the AWS Management Console: AWS Console
#### In the search bar, type "S3" and select S3 from the services list.

## Step 2: Create an S3 Bucket
#### Click "Create bucket" (top-right corner).
#### Bucket Name: Enter a unique bucket name (e.g., poc-s3-bucket).
#### AWS Region: Select the region where you want the bucket to be created (e.g., us-east-1).
#### Bucket Settings:
#### Block Public Access (Recommended: Keep default settings to block public access).
#### Versioning (Optional: Enable if you want to keep versions of files).
#### Server-side Encryption (Choose AES-256 for default encryption).
#### Click Create bucket.

## Step 3: Upload a File to S3 Bucket
#### Click on the newly created bucket (poc-s3-bucket).
#### Click "Upload".
#### Click "Add files" and select a file from your system.
#### (Optional) Click "Add folder" if you want to upload an entire folder.
#### Storage class: Keep the default (Standard) unless you need cost optimization.
#### Click Upload.

#### Step 4: Verify File Upload
#### Navigate to the Objects tab inside your bucket.
#### Verify that the uploaded file appears in the list.
#### Click on the file name to see the Object URL (useful for accessing the file).

## ✅ Your S3 bucket is now created successfully, and the file is uploaded! 🎉
