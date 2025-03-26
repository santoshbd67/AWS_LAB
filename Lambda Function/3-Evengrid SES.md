# 🚀 Automatically Stop EC2 via Email Using S3 + SNS + Lambda  

## 🔹 How It Works  
1. **Gmail → AWS WorkMail**: Email is forwarded to AWS WorkMail.  
2. **WorkMail → S3**: The email is stored as a file in an S3 bucket.  
3. **S3 → SNS**: S3 triggers an SNS notification when a new file is uploaded.  
4. **SNS → Lambda**: SNS invokes a Lambda function.  
5. **Lambda → EC2**: Lambda reads the email, and if it contains `"Stop the EC2 instance"`, it stops the EC2 instance.  

---

## ✅ Step 1: Create an S3 Bucket to Store Emails  
1. **Go to AWS Console** → Open **S3** → Click **Create Bucket**.  
2. **Enter Bucket Name**: `email-storage-bucket`.  
3. **Choose Region**: `us-east-1` (or your preferred region).  
4. **Disable Block Public Access** (not needed for this use case).  
5. Click **Create Bucket**.  

✅ **S3 is now ready to store emails.**  

---

## ✅ Step 2: Set Up AWS WorkMail to Receive Emails  
1. Go to **AWS WorkMail Console** → Click **Organizations**.  
2. Click **Create Organization** → Select **WorkMail** → Click **Next**.  
3. Choose your AWS **Region** and click **Next**.  
4. Enter a name (e.g., `myemail-org`) and click **Create Organization**.  
5. **Wait for WorkMail to be ready** (this may take a few minutes).  

### **Create a WorkMail Email Address**  
1. **Go to AWS WorkMail Console** → Click **Users**.  
2. Click **"Create User"**.  
3. **Username**: `stop` (This creates `stop@yourdomain.com`).  
4. **Set Password** and **Create User**.  

✅ **Your email address (`stop@yourdomain.com`) is ready.**  

---

## ✅ Step 3: Configure Email Forwarding to S3  
1. **Go to WorkMail Console** → Click **Email Flow** → Click **Rules**.  
2. Click **Create Rule**.  
3. **Rule Name**: `ForwardToS3`.  
4. **Condition**: If recipient is **stop@yourdomain.com**.  
5. **Action**: `Deliver to Amazon S3`.  
6. **S3 Bucket**: Choose `email-storage-bucket`.  
7. Click **Save Rule**.  

✅ **Now, any email sent to `stop@yourdomain.com` is saved in S3.**  

---

## ✅ Step 4: Create an SNS Topic  
1. Go to **AWS SNS Console** → Click **"Create Topic"**.  
2. **Topic Name**: `s3-email-events`.  
3. **Type**: **Standard**.  
4. Click **Create Topic**.  

### **Subscribe Lambda to SNS**  
1. Go to **AWS SNS Console** → Click **`s3-email-events`** topic.  
2. Click **"Create Subscription"**.  
3. **Protocol**: Choose **AWS Lambda**.  
4. **Endpoint**: Select **`StopEC2Instance`** Lambda function.  
5. Click **Create Subscription**.  

✅ **SNS will now notify Lambda when it receives a message.**  

---

## ✅ Step 5: Configure S3 to Send Notifications to SNS  
1. Go to **AWS S3 Console** → Click **`email-storage-bucket`**.  
2. Click **Properties** → Scroll to **Event Notifications**.  
3. Click **"Create Event Notification"**.  
4. **Event Name**: `EmailUploadTrigger`.  
5. **Event Type**: **Put (Object Created)**.  
6. **Destination**: Choose **SNS Topic**.  
7. Select **`s3-email-events`**.  
8. Click **Save Changes**.  

✅ **Now, S3 will notify SNS when a new email file is uploaded.**  

---

## ✅ Step 6: Modify Lambda to Process SNS Messages  
1. Go to **AWS Lambda Console** → Click `StopEC2Instance`.  
2. Click **Edit Code** and replace the existing code with:

```python
import boto3
import json

# Initialize AWS Clients
s3 = boto3.client('s3')
ec2 = boto3.client('ec2', region_name='us-east-1')  # Change region if needed

# Your EC2 Instance ID
INSTANCE_ID = "i-xxxxxxxxxxxxxxxxx"  # Replace with your EC2 Instance ID

def lambda_handler(event, context):
    for record in event['Records']:
        # SNS message contains S3 event details
        sns_message = json.loads(record['Sns']['Message'])
        bucket_name = sns_message['Records'][0]['s3']['bucket']['name']
        object_key = sns_message['Records'][0]['s3']['object']['key']

        # Read email content from S3
        email_obj = s3.get_object(Bucket=bucket_name, Key=object_key)
        email_content = email_obj['Body'].read().decode('utf-8')

        # Check if email subject contains "Stop the EC2 instance"
        if "Stop the EC2 instance" in email_content:
            print(f"Stopping EC2 Instance: {INSTANCE_ID}")
            ec2.stop_instances(InstanceIds=[INSTANCE_ID])
            return {"statusCode": 200, "body": f"EC2 {INSTANCE_ID} stopped"}
    
    return {"statusCode": 400, "body": "No action taken"}
```
---

Click **Deploy**.

### ✅ Lambda now listens for SNS events and stops EC2 when an email is received.



