# Stop an EC2 Instance Using AWS Lambda Function

#### This Proof of Concept (POC) demonstrates how to automatically stop an EC2 instance using an AWS Lambda function triggered manually or via a scheduled event.

## Step 1: Create an IAM Role for Lambda
#### Login to AWS Console → Navigate to IAM.

#### Click Roles → Create Role.
<img width="934" alt="image" src="https://github.com/user-attachments/assets/87f7775d-f2e9-4b43-895b-c471df4fff14" />

#### Select Use Case → Choose AWS Service → Select Lambda.

#### Click Next: Permissions.
<img width="950" alt="image" src="https://github.com/user-attachments/assets/bfdc7c3e-0e30-4028-9654-81c02d87a7ca" />

#### Attach the following policy:

#### AmazonEC2FullAccess (or create a custom policy with least privileges).

#### Click Next → Name the Role (e.g., Lambda_EC2_Stop_Role).
<img width="951" alt="image" src="https://github.com/user-attachments/assets/d627bdd2-957a-488f-a9e7-a0dbc117b43b" />

#### Click Create Role.

## Step 2: Create a Lambda Function
#### Go to AWS Console → Navigate to Lambda.

#### Click Create Function.
<img width="950" alt="image" src="https://github.com/user-attachments/assets/a9e44add-d641-40d5-a459-3201a11b1b14" />

#### Choose Author from scratch.

#### Function Name: StopEC2Instance.

#### Runtime: Select Python 3.9 (or latest).
<img width="933" alt="image" src="https://github.com/user-attachments/assets/0fe7f73f-425c-4689-a181-78245b2dd7d0" />

#### Permissions: Choose Use an existing role → Select Lambda_EC2_Stop_Role.

#### Click Create Function.
<img width="929" alt="image" src="https://github.com/user-attachments/assets/c4e1aea1-8274-496a-a1ec-cc8f0a1b2602" />

## Step 3: Add the Python Code to Stop EC2 Instance
#### Scroll down to the Code Source section.

#### Click Edit Code and replace the default code with:
```
import boto3

def lambda_handler(event, context):
    ec2 = boto3.client('ec2', region_name='us-east-1')  # Change region if needed
    
    instance_id = "i-xxxxxxxxxxxxxxxxx"  # Replace with your EC2 Instance ID
    
    try:
        response = ec2.stop_instances(InstanceIds=[instance_id])
        return {
            'statusCode': 200,
            'body': f'EC2 Instance {instance_id} stopped successfully'
        }
    except Exception as e:
        return {
            'statusCode': 500,
            'body': f'Error: {str(e)}'
        }
```
#### Modify the instance_id with your actual EC2 instance ID.
<img width="936" alt="image" src="https://github.com/user-attachments/assets/0d9fcfef-b86d-4318-abc2-63bf1a665c6a" />
#### Click Deploy.

## Step 4: Test the Lambda Function
#### Click Test → Create a new test event.

#### Event Name: StopEC2Test.

#### Leave the default JSON input.

#### Click Create → Click Test again.

#### If successful, you will see:

#### EC2 Instance i-xxxxxxxxxxxxxxxxx stopped successfully

### ✅ Verify in EC2 Dashboard that the instance is stopped.

## Step 5 (Optional): Automate Using CloudWatch Event Rule
#### To automate EC2 shutdown at a specific time:

#### Go to AWS Console → Navigate to Amazon EventBridge (formerly CloudWatch Events).

#### Click Rules → Create Rule.

#### Name: StopEC2Schedule.

#### Event Source: Select Schedule.

#### Fixed Rate or Cron Expression:

#### Example cron for stopping EC2 every night at 10 PM UTC:
```
0 22 * * ? *
```
#### Target: Choose AWS Lambda function → Select StopEC2Instance.

#### Click Create Rule.

## Step 6: Verify the Automation
#### Wait for the scheduled time or trigger manually via Test.

#### Check the EC2 Dashboard to confirm the instance is stopped.

## Conclusion
#### You have successfully created an AWS Lambda function to stop an EC2 instance, either manually or automatically via EventBridge scheduling. 🚀

