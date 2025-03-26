🚀 Final Workflow
Amazon SES receives an email at ec2-stop@yourdomain.com.

SES forwards the email to Amazon SNS.

SNS triggers a Lambda function (ProcessEmailSNS).

Lambda (ProcessEmailSNS) extracts the subject from the email.

If the subject contains "Stop the EC2 instance", it invokes your existing Lambda function (StopEC2Instance).

EC2 instance stops automatically. 🚀

✅ Step 1: Verify a Domain in Amazon SES
Why?
SES needs a verified domain to receive emails.

Steps to Verify a Domain
Go to AWS SES Console → Click Verified Identities.

Click Create Identity → Select Domain.

Enter your domain name (e.g., yourdomain.com).

AWS will provide TXT, MX, and CNAME records.

Add these records to your domain provider (GoDaddy, Route 53, etc.).

Wait for verification completion (~10-30 minutes).

Enable Email Receiving.

✅ Now SES can receive emails for this domain.

✅ Step 2: Create an SNS Topic
Why?
SNS allows SES to forward emails and trigger Lambda.

Steps to Create SNS Topic
Go to AWS SNS Console → Click Topics.

Click Create Topic.

Choose Standard Topic.

Topic Name: EC2StopEmailTrigger

Click Create Topic.

✅ SNS topic is ready.

✅ Step 3: Subscribe Lambda to the SNS Topic
Why?
SNS needs to trigger a Lambda function when an email arrives.

Steps to Subscribe a Lambda Function
Open Amazon SNS.

Click on EC2StopEmailTrigger topic.

Click Create Subscription.

Protocol: Choose AWS Lambda.

Endpoint: Select your Lambda function (ProcessEmailSNS).

Click Create Subscription.

✅ SNS can now trigger Lambda.

✅ Step 4: Configure SES to Forward Emails to SNS
Why?
SES needs to forward incoming emails to SNS.

Steps to Create an SES Rule
Go to AWS SES → Click Rule Sets.

Click Create Rule Set.

Click Create Rule.

Set Recipient Condition

Enter "ec2-stop@yourdomain.com".

Add an Action

Click Add Action → Choose Amazon SNS.

Select the SNS Topic: EC2StopEmailTrigger.

Click Create Rule.

Enable the Rule Set.

✅ Now, SES forwards emails to SNS.

✅ Step 5: Create the Lambda Function to Process Email
Why?
This Lambda function will parse the email subject and invoke your existing StopEC2Instance Lambda.

Steps to Create Lambda
Go to AWS Lambda Console → Click Create Function.

Choose "Author from scratch".

Function Name: ProcessEmailSNS

Runtime: Choose Python 3.9.

Permissions:

Click Change default execution role → Create a new role.

Attach AmazonSNSFullAccess and AWSLambdaBasicExecutionRole.

Click Create Function.

✅ Lambda function created.

✅ Step 6: Add Lambda Function Code
Why?
This code reads the email subject and invokes your existing EC2 Stop Lambda function.

Steps to Add Code
Open AWS Lambda → ProcessEmailSNS function.

Go to the Code tab.

Replace the default code with:

python
Copy
Edit
import json
import boto3

lambda_client = boto3.client('lambda')

EC2_STOP_LAMBDA = "StopEC2Instance"  # Replace with your existing Lambda function name

def lambda_handler(event, context):
    print("Received event: " + json.dumps(event, indent=2))

    # Extract email message from SNS
    for record in event['Records']:
        message = json.loads(record["Sns"]["Message"])
        subject = message.get("mail", {}).get("commonHeaders", {}).get("subject", "")

        if "Stop the EC2 instance" in subject:
            # Invoke the existing EC2 stop Lambda function
            response = lambda_client.invoke(
                FunctionName=EC2_STOP_LAMBDA,
                InvocationType='Event'  # Async invocation
            )
            return {
                'statusCode': 200,
                'body': 'Triggered EC2 Stop Lambda'
            }

    return {
        'statusCode': 400,
        'body': 'No action taken'
    }
Click Deploy.

✅ Lambda function is ready.

✅ Step 7: Test the Setup
How to Test?
Send an email to "ec2-stop@yourdomain.com".

Subject: "Stop the EC2 instance".

Check AWS Lambda logs:

Open AWS Lambda → ProcessEmailSNS → Monitor → Logs.

If the subject is correct, EC2 instance should stop.

✅ EC2 instance stops successfully! 🚀

🎯 Summary
✅ Amazon SES receives an email.
✅ SES forwards email to SNS.
✅ SNS triggers Lambda (ProcessEmailSNS).
✅ Lambda reads the email subject.
✅ If the subject matches, it triggers your existing Lambda function (StopEC2Instance).
✅ EC2 instance stops automatically! 🚀

This fully automated event-driven system requires no S3 storage and is instantaneous. 🎉

✨ Next Steps (Optional)
Enable notifications when EC2 stops

Modify your StopEC2Instance Lambda to send an email via SNS.

Extend the system to start EC2

Modify the ProcessEmailSNS Lambda to handle "Start the EC2 instance".

Improve security

Restrict SES to accept emails only from trusted senders.

Would you like help setting up SNS notifications for successful EC2 shutdowns? 😊
