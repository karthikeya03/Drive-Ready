# Creatng a RDS database and connecting it with a Ec2 instnace : 

## Step 1: Creating an RDS Database

1. **Go to Dashboard, Select RDS:**

   - Sign in to the [AWS Management Console](https://aws.amazon.com/console/).
   - In the console, search for "RDS" in the services search bar and select "RDS" from the dropdown.

2. **Create a Database:**

   - Click on the "Create database" button.

3. **Select Standard Create:**

   - Under "Database creation method," select "Standard create" for more customization options.

     ![image](https://github.com/user-attachments/assets/ceb00cb3-8b47-4072-9df7-9d337c0779d3)

4. **Select MySQL:**

   - In the "Engine options" section, choose "MySQL" as the database engine.

![image](https://github.com/user-attachments/assets/69875d8f-a85a-49b9-be58-1d65a42cc679)

5. **Select Free Tier:**
   - In the "Templates" section, select "Free tier" to stay within the free tier limits.
     ![image](https://github.com/user-attachments/assets/66cefd7a-dfe2-4114-8541-ab400d6df1a8)

6. **Give Database Name and Password:**
   - **DB instance identifier:** Enter a unique name for your RDS instance.
   - **Master username:** Enter a username.
   - **Master password:** Enter a password and confirm it.

![image](https://github.com/user-attachments/assets/b7142f07-d4af-42f1-b3b2-3992898064ff)

7. **Allow Public Access:**

   - In the "Connectivity" section, set "Publicly accessible" to "Yes" if you want to access the database from outside the VPC.

8. **Create:**

   - Review all the settings to ensure they are correct.

   - Click on the "Create database" button to launch the RDS instance.

     ![image](https://github.com/user-attachments/assets/00a653ec-2ccd-4b60-8d98-06548a40b289)

## Step 2: Creating an Ubuntu EC2 Instance

1. **Go to EC2 Dashboard:**
   - In the AWS Management Console, search for "EC2" and select it from the services dropdown.

2. **Launch Instance:**
   - Click the "Launch instance" button.

3. **Choose an Amazon Machine Image (AMI):**
   - Select "Ubuntu Server 20.04 LTS" from the list of available AMIs.

4. **Choose an Instance Type:**
   - Select an instance type (e.g., `t2.micro` if you are using the free tier).

5. **Configure Instance Details:**
   - Configure the instance details as needed, such as the number of instances, network settings, and IAM roles.

6. **Add Storage:**
   - Specify the storage size and type. The default settings are usually sufficient for a basic setup.

7. **Add Tags:**
   - (Optional) Add tags to your instance for easier identification.

8. **Configure Security Group:**
   - Create a new security group or select an existing one.
   - Add rules to allow necessary traffic (e.g., SSH, HTTP/HTTPS).

9. **Review and Launch:**
   - Review all the settings.
   - Click the "Launch" button.

10. **Select Key Pair:**
    - Choose an existing key pair or create a new one to access your instance.
    - Download the key pair file (.pem) if you created a new one.

11. **Launch Instances:**
    - Click the "Launch Instances" button to start your EC2 instance.

## Notes:

- **Security Group:** Ensure your security group allows inbound traffic on the necessary ports (e.g., port 22 for SSH, port 3306 for MySQL).
- **Key Pair:** Keep your key pair file secure. You'll need it to connect to your EC2 instance via SSH.
- **Public IP:** If your instance needs to be accessible from the internet, make sure it has a public IP address.
- **IAM Roles:** Use IAM roles to manage permissions for your instances securely.

## Step 3: Connect through MobaXterm

1. **Download and Install MobaXterm:**
   - Download MobaXterm from the [official website](https://mobaxterm.mobatek.net/).
   - Install and launch MobaXterm.

2. **Connect to EC2 Instance:**
   - In MobaXterm, click on the "Session" icon.
   - Select "SSH" as the session type.
   - Enter the public IP address of your EC2 instance.
   - Use the key pair file (.pem) for authentication:
     - Go to the "Advanced SSH settings" tab.
     - Browse and select your key pair file.
   - Click "OK" to connect.

## Step 4: Update Package Lists

1. **Run the update command:**

   - In the MobaXterm terminal, execute the following command to update the package lists:

     ```
     sudo apt-get update
     ```

## Step 5: Install MySQL Client

1. **Install the MySQL client:**

   - After updating the package lists, install the MySQL client by running:

     ```
     sudo apt-get install mysql-client
     ```

2. **Verify Installation:**

   - Confirm the installation by checking the MySQL client version:

     ```
     mysql --version
     ```

## Step 5: Connect to RDS Endpoint

1. **Get the RDS Endpoint Link:**
   - In the AWS Management Console, go to the RDS dashboard.
   - Select your RDS instance and find the endpoint link in the "Connectivity & security" section.

2. **Connect to the RDS Database:**
   - In the MobaXterm terminal, use the following command to connect to your RDS database:
     ```
     mysql -h <rds-endpoint-link> -u <username> -p
     ```
3. **Select the database **:
   ![image](https://github.com/user-attachments/assets/5294f3e9-c634-4577-9094-74634c1fad4a)
   - set up Ec2 connection
   ![image](https://github.com/user-attachments/assets/2ca49459-8cd9-4ffc-949f-70f2a2d8d97f)

it will look like this : 

![image](https://github.com/user-attachments/assets/f62a65a4-cd66-48b3-8e20-be548d808d2d)

**Note:** Replace `<rds-endpoint-link>` with your actual RDS endpoint link and `<username>` with your master username.

After connecting : 
![image](https://github.com/user-attachments/assets/6d2d9f4d-b704-47b8-b04a-7d9de3ecf85a)

## Notes:

- **Security Group:** Ensure your security group allows inbound traffic on the necessary ports (e.g., port 22 for SSH, port 3306 for MySQL).
- **Key Pair:** Keep your key pair file secure. You'll need it to connect to your EC2 instance via SSH.
- **Public IP:** If your instance needs to be accessible from the internet, make sure it has a public IP address.
- **IAM Roles:** Use IAM roles to manage permissions for your instances securely.

# Connecting through MySQL Workbench :


![MySQL Workbench Home](https://github.com/user-attachments/assets/93a861eb-47e0-4674-a702-0bbb113e0548)

![New Connection Setup](https://github.com/user-attachments/assets/25f20e70-f730-4379-8057-f0f2f49a0571)

![Connection Details](https://github.com/user-attachments/assets/a91a759e-2135-4e32-a38d-2a8c45d24803)



