# Deploy a Static Website on AWS S3

## Step 1: Create an S3 Bucket

#### Login to AWS Console → Navigate to S3.

#### Click Create Bucket.

#### Enter a unique bucket name (e.g., devops-training-site).

#### Choose a region (e.g., us-east-1).

#### Uncheck "Block all public access" → Confirm by typing "confirm".
<img width="939" alt="image" src="https://github.com/user-attachments/assets/10c52657-33a4-4a5f-8632-4d65222a1153" />

#### Leave other settings as default → Click Create bucket.


## Step 2: Upload Website Files

#### Open your S3 bucket → Click Upload.

#### Click Add Files → Select index.html.

#### Click Upload.

## Step 3: Enable Static Website Hosting

#### Open the S3 bucket → Go to Properties.

#### Scroll down to Static website hosting → Click Edit.

#### Select "Enable".

#### Set Index document to:
```
index.html
```

#### Click Save changes.

## Step 4: Set Public Access Permissions

#### Modify Bucket Policy
#### Go to Permissions → Scroll to Bucket policy.

#### Click Edit → Copy and paste the following policy:
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::devops-training-site/*"
    }
  ]
}
```
#### (Replace devops-training-site with your bucket name.)

#### Click Save changes.

## Step 5: Access the Website

#### Go to S3 → Your Bucket → Properties.

#### Scroll to Static website hosting.

#### Copy the Bucket website endpoint (e.g.,
```
http://devops-training-site.s3-website-us-east-1.amazonaws.com
```
#### Open the URL in a browser.

### ✅ Your website should now display:
### "Welcome to the DevOps Training" with a background image.
