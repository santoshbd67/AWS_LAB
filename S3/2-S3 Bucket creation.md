# 🔹 Step-by-Step Guide to Create an S3 Bucket and Upload a File (Using AWS Console UI) for POC

## Step 1: Sign in to AWS Management Console
#### Open the AWS Management Console: AWS Console
#### In the search bar, type "S3" and select S3 from the services list.

## Step 2: Create an S3 Bucket
#### Click "Create bucket" (top-right corner).
<img width="948" alt="image" src="https://github.com/user-attachments/assets/0c0fd100-5a8e-4d06-8b82-965a62712603" />

#### Bucket Name: Enter a unique bucket name (e.g., poc-s3-bucket).
<img width="749" alt="image" src="https://github.com/user-attachments/assets/0e379c6d-ddc8-4a0e-99aa-a8ce818282dc" />

#### AWS Region: Select the region where you want the bucket to be created (e.g., us-east-1).
#### Bucket Settings:
#### Block Public Access (Recommended: Keep default settings to block public access).
<img width="823" alt="image" src="https://github.com/user-attachments/assets/b610f85d-b1d1-41c8-9d20-108d6ffee638" />

#### Versioning (Optional: Enable if you want to keep versions of files).
#### Server-side Encryption (Choose AES-256 for default encryption).
#### Click Create bucket.
<img width="938" alt="image" src="https://github.com/user-attachments/assets/864339de-600e-4c96-bb0c-ef8154b1bbf9" />

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
