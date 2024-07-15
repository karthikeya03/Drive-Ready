# AWS SDK and Ways to Access AWS Services

## AWS SDK :

The AWS SDK (Software Development Kit) provides a set of tools and libraries that enable developers to interact with AWS services using their preferred programming languages. AWS SDKs are available for various programming languages, such as:

- Java
- Python
- JavaScript (Node.js)
- .NET (C#)
- Ruby
- PHP
- Go
- C++

Each SDK includes:

- Libraries for AWS services
- Code examples
- Documentation
- Developer tools

## Accessing AWS Services

There are several ways to access and manage AWS services:

### AWS Management Console

The AWS Management Console is a web-based interface that allows you to manage and interact with AWS services. It provides a user-friendly way to create, configure, and monitor AWS resources.

### AWS Command Line Interface (CLI)

The AWS CLI is a unified tool to manage AWS services. With just one tool to download and configure, you can control multiple AWS services from the command line and automate them through scripts. To install the AWS CLI, follow these steps:

1. Download and install the AWS CLI from the [AWS CLI installation page](https://aws.amazon.com/cli/).
2. Configure the AWS CLI using the command:
   \`\`\`bash
   aws configure
   \`\`\`

### AWS SDKs

AWS SDKs provide a more programmatic way to interact with AWS services using your preferred programming languages. For example, using the AWS SDK for Python (Boto3):

\`\`\`python
import boto3

# Create an S3 client
s3 = boto3.client('s3')

# List all buckets
response = s3.list_buckets()
for bucket in response['Buckets']:
    print(bucket['Name'])
\`\`\`

### Boto3

Boto3 is the AWS SDK for Python. It allows Python developers to interact with AWS services like S3, EC2, DynamoDB, and more. To install Boto3, use pip:

\`\`\`bash
pip install boto3
\`\`\`

Here's an example of how to use Boto3 to upload a file to an S3 bucket:

\`\`\`python
import boto3

s3 = boto3.client('s3')
s3.upload_file('local_file.txt', 'my_bucket', 's3_file.txt')
\`\`\`

## AWS Cloud9 Integrated Development Environment (IDE)

AWS Cloud9 is a cloud-based integrated development environment (IDE) that lets you write, run, and debug your code with just a browser. It includes a code editor, debugger, and terminal. Cloud9 is integrated with AWS, so you can easily access and manage your AWS resources from within the IDE.

### Features of AWS Cloud9

- **Code with ease**: The Cloud9 IDE offers a rich code-editing experience with support for several programming languages.
- **Collaborate in real-time**: Multiple developers can work on the same codebase and see each other's changes in real time.
- **Preconfigured environment**: Cloud9 comes with essential tools pre-installed, so you can start coding right away without worrying about setup.
- **Terminal access**: Direct terminal access to your AWS resources.
- **Integrated with AWS**: Directly access AWS services and resources from the IDE.

### Accessing AWS Cloud9

1. Sign in to the [AWS Management Console](https://aws.amazon.com/console/).
2. Navigate to the Cloud9 service.
3. Create a new Cloud9 environment and configure its settings.
4. Start using the Cloud9 IDE to write, run, and debug your code.

# Process for Setting Up and Using AWS CloudShell and AWS Cloud9

## Overview and Objectives

This process guides you through connecting to AWS CloudShell, exploring its capabilities, launching an AWS Cloud9 instance, and using Amazon CodeWhisperer to generate a Python script.

## Step 1: Exploring AWS CloudShell

1. **Connect to AWS CloudShell**

   - Open the AWS Management Console.
   - Choose the AWS CloudShell icon at the top of the screen.
   - A new browser tab opens with the AWS CloudShell interface.
   - Close the "Welcome to AWS CloudShell" pop-up window if it appears.
   - Wait for the terminal to become available.

  ![image](https://github.com/karthikeya03/Drive-Ready/assets/120096427/779adec5-ccb1-4e5b-ab83-a54d702da317)


2. **Verify AWS CLI Installation**

   - Run the command: `aws --version`
   - Ensure the output shows AWS CLI version 2.x.x.
     ![image](https://github.com/karthikeya03/Drive-Ready/assets/120096427/08c1b396-7f63-4af5-84d6-80f3fd93649f)


3. **List S3 Buckets**

   - Run the command: `aws s3 ls`
   - Note the list of S3 buckets.

4. **Open Multiple Terminal Panels**

   - From the Actions menu, choose Tabs layout > Split into columns.

5. **Upload and Run Python Script**

   - Download the `list-buckets.py` file from [HERE](https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-200-ACCDEV-2-91558/01-lab-cloud9/s3/list-buckets.py)
   - Upload the file to CloudShell.
   - Run the command: `cat list-buckets.py`
     
     ![image](https://github.com/karthikeya03/Drive-Ready/assets/120096427/5bf781ea-64ef-4bbd-ae09-477f7940afb5)

   - Run the script: `python3 list-buckets.py`
   - Note the list of S3 buckets.

6. **Copy File to S3 Bucket**

   - Run the command: `aws s3 cp list-buckets.py s3://<bucket-name>`
   - Verify the upload was successful.

![image](https://github.com/karthikeya03/Drive-Ready/assets/120096427/e47864ba-6150-4af3-9756-cff9669e0c1b)


## Step 2: Creating an AWS Cloud9 Instance

1. **Open AWS Cloud9**

   - In the AWS Management Console, search for and choose Cloud9.

2. **Create Environment**

   - Choose Create environment.
   - Name the environment `MyCloud9`.
   - Choose Additional Instance Types > t2.medium.
   - In the New EC2 instance section, choose Additional Instance Types.
   - From the Additional instance types dropdown list, choose t2.medium.
   - Set Network settings to Secure Shell (SSH).
   - Choose Create.

![image](https://github.com/karthikeya03/Drive-Ready/assets/120096427/cf8a3c1c-5b64-48c5-b01b-bf7c1874b05c)


3. **Open AWS Cloud9 IDE**

   - Choose the Open link to open your AWS Cloud9 IDE.

## Step 3: Exploring AWS Cloud9 IDE

1. **Copy File from S3 to Cloud9**

   - Run the command: `aws s3 cp s3://<bucket-name>/list-buckets.py .`
   - Verify the file appears in the navigation pane.

2. **Run Python Script**

   - Double-click `list-buckets.py` to open it.
   - Ensure Python is the chosen syntax.
   - Run the script using the Run icon.
   - Install boto3 if necessary: `sudo pip3 install boto3`
   - Verify the script runs successfully.

3. **Create and Upload HTML File**

   - Create a new HTML file with "Hello World" text.
   - Save the file as `index.html`.
   - Upload the file to S3 using AWS Explorer.

## Step 4: Using Amazon CodeWhisperer

1. **Enable CodeWhisperer**

   - In AWS Explorer, expand CodeWhisperer.
   - Ensure Auto-Suggestions is running.

2. **Generate Python Script**

   - Create a new Python file.
   - Add the following code and comments to generate suggestions:

   ```python
   import boto3
   
   BUCKET_NAME = '<bucket-name>'
   FILE_NAME = 'index.html'
   
   # setup s3 client named s3_client
   # create a function to put s3 bucket ownership controls with Rules set to BucketOwnerPreferred
   # create a function to set public access block values to false
   # create a function to allow public access to FILE_NAME
   # call the functions
   ```

   - Accept the suggestions provided by CodeWhisperer.

3. **Save and Run Script**

   - Save the script as `s3-permissions.py`.
   - Run the script using the Run icon.
   

## Verification

1. **Check Webpage Accessibility**
   - In the AWS Management Console, navigate to the S3 bucket.
   -  give read-write permissions for that object
   - Open the `index.html` file using the Object URL.
   - Verify the "Hello World" message is displayed.

## Conclusion

You have successfully explored AWS CloudShell and AWS Cloud9, copied files between S3 and CloudShell/Cloud9, installed and used boto3, created a simple webpage, and used Amazon CodeWhisperer to generate Python code.
