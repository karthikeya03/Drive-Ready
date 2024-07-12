# Objective: Create a static website using Amazon S3 and apply architectural best practices

## Task 1: Connecting to the AWS Cloud9 IDE and configuring the environment

1. Connect to the AWS Cloud9 IDE:
   - From the Services menu, search for and select Cloud9.
   - Choose the existing IDE named Cloud9 Instance and select Open.

2. Install the AWS SDK for Python:
   - In the AWS Cloud9 bash terminal, run: `sudo pip install boto3`

  ![image](https://github.com/user-attachments/assets/1ccddd87-44b0-4e8e-8aae-0faa17ca136c)

3. Download and extract the required files:
   - Run: `wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-200-ACCDEV-2-91558/02-lab-s3/code.zip -P /home/ec2-user/environment`
   - Extract the file: `unzip code.zip`.

4. Verify the AWS CLI version 2:
   - Run: `aws --version`.

## Task 2: Creating an S3 bucket using the AWS CLI

1. Create an S3 bucket:
   - Run: `aws s3api create-bucket --bucket <bucket-name> --region us-east-1`.
   - Example bucket name: `<initials>-<YYYY-MM-DD>-s3site`.

2. Confirm the bucket creation:
   - In the AWS Management Console, go to Services > S3.
   - Verify that the bucket is created with `Bucket and objects not public`.

3. Edit public access settings:
   - Choose the bucket name and select Permissions.
   - Edit and de-select `Block all public access`, save changes.

![image](https://github.com/user-attachments/assets/bf7952a7-cf1d-4034-912d-9c94ad638b32)

## Task 3: Setting a bucket policy using the SDK for Python

1. Create the policy document:
   - In AWS Cloud9 IDE, create a file named `website_security_policy.json` and paste the policy JSON.
   - Replace `<bucket-name>` with your bucket name and `<ip-address>` with your IP address.

  ![image](https://github.com/user-attachments/assets/8f3e5509-91ce-4d22-b3d2-dc3b32056612)


2. Apply the bucket policy using the SDK for Python:
   - In the navigation pane, expand the `python_3` directory and open `permissions.py`.
   - Replace `<bucket-name>` with your bucket name and save the changes.
   - In the terminal, run: `cd python_3` and `python3 permissions.py`.

## Task 4: Uploading objects to the bucket to create the website

1. Upload the website files:
   - Run: `aws s3 cp ../resources/website s3://<bucket-name>/ --recursive --cache-control "max-age=0"`.

## Task 5: Testing access to the website

1. Load the website:
   - In the S3 console, choose your bucket name and select Objects.
   - Choose the `index.html` file and copy the Object URL.
   - Verify the website by pasting the URL into your browser.

2. Test access from outside your network:
   - Try loading the URL on a mobile phone with a cellular network or run `curl https://<bucket-name>.s3.amazonaws.com/index.html` in the AWS Cloud9 terminal.

## Task 6: Analyzing the website code

1. Review the website code in AWS Cloud9 IDE:
   - Open the `index.html`, `config.js`, `pastries.js`, and `all_products.json` files.
   - Understand the structure and logic of the website code.

![Uploading image.png…]()
