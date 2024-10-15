DOCKER : 

IF YOU RUN AN IMAGE IT BEOCMES A CONTAINER

IF THE OS IS ON YOUR PENDIRVE ITS AN IMAGE

IF ITS RUNNED INTO UPUR COMPUTER THEN ITS A CONTIANER

SEARCH FOR MONGO

Step 1: Launch an Ubuntu Instance
Go to the AWS EC2 Dashboard:

Open the AWS Management Console.
Navigate to EC2 by searching for "EC2" in the search bar.
Launch an EC2 Instance:

Click on Launch Instance.
Choose AMI: Select Ubuntu Server 20.04 LTS (free tier eligible).
Instance Type: Select t2.micro (free tier eligible).
Key Pair: If you don't have a key pair, create one for SSH access.
Configure Storage: The default size is 8GB, but you can modify it if needed.
Security Group: Allow SSH (port 22) for access and HTTP/HTTPS if you plan to expose a web app.
Launch the instance.
Connect to Your Instance:

Once the instance is running, click on Connect.
Copy the provided SSH command and use it to connect from your terminal:
bash
Copy code
ssh -i /path/to/your-key.pem ubuntu@<your-ec2-public-ip>
Step 2: Update Ubuntu
Once connected to your instance:

Update package list:

bash
Copy code
sudo apt update
Upgrade installed packages:

bash
Copy code
sudo apt upgrade -y




step 2 :  isntall docker
Install Docker
Install Docker with a Single Command: Run the following command to install Docker:

bash
Copy code
curl -fsSL https://get.docker.com/ | sh
Start the Docker Service: After installation, start the Docker service using:

bash
Copy code
sudo systemctl start docker
Enable Docker to Start at Boot: To ensure Docker starts automatically on system boot, run:

bash
Copy code
sudo systemctl enable docker
Verify Docker Installation: You can verify that Docker was installed correctly by running:

bash
Copy code
sudo docker --version
This command will show you the installed version of Docker.

Run a Test Container: To confirm that Docker is working properly, you can run a simple test container:

bash
Copy code
sudo docker run hello-world
If Docker is installed correctly, you should see a message saying "Hello from Docker!" and information about how to use Docker.


Step 4: Enable SSH and Port Number
To ensure that you can access your MongoDB instance securely and that the necessary ports are open, you’ll need to configure both the security group in AWS and the firewall on your Ubuntu server.

4.1: Configure AWS Security Group
Log into the AWS Management Console.

Navigate to EC2 Dashboard:

Click on "Instances" in the left sidebar.
Find your running instance and click on its Instance ID.
Edit Security Groups:

Scroll down to the "Security" tab.
Under "Security Groups", click on the security group link.
Add Inbound Rules:

Click on the "Inbound rules" tab.
Click on "Edit inbound rules".
Add the following rules:
SSH:
Type: SSH
Protocol: TCP
Port Range: 22
Source: Your IP (or 0.0.0.0/0 for all, though this is less secure).
MongoDB:
Type: Custom TCP
Protocol: TCP
Port Range: 27017
Source: Your IP (or 0.0.0.0/0 for all, again less secure).
Click "Save rules".
Note: Allowing access from 0.0.0.0/0 can expose your MongoDB to the internet, which is not recommended for production environments. Always restrict it to specific IP addresses whenever possible.

4.2: Configure the Firewall on Ubuntu
Check the UFW Status: To see if the firewall (UFW - Uncomplicated Firewall) is active, run:

bash
Copy code
sudo ufw status
Enable UFW (if not already enabled): If UFW is not enabled, you can enable it with:

bash
Copy code
sudo ufw enable
Allow SSH and MongoDB Ports: Run the following commands to allow traffic on the SSH and MongoDB ports:

bash
Copy code
sudo ufw allow 22/tcp   # Allow SSH
sudo ufw allow 27017/tcp  # Allow MongoDB
Verify UFW Rules: After adding the rules, check the status again:

![image](https://github.com/user-attachments/assets/d73c65aa-7169-4c1a-b6f2-c41fca1bc168)

bash
Copy code
sudo ufw status
Summary of Step 4
Configured AWS Security Group to allow inbound traffic on SSH (port 22) and MongoDB (port 27017).
Configured UFW on Ubuntu to allow traffic on the same ports.
Step 5: Verify MongoDB Container is Running
Check if the MongoDB container is running:
bash
Copy code
docker ps
Step 6: Access MongoDB from Your Host
Connect to MongoDB using a MongoDB client or shell:
For command-line access, run:
bash
Copy code
mongo --host 54.242.25.192 --port 27017 -u admin -p pass --authenticationDatabase admin
Step 7: Stop and Remove the MongoDB Container (Optional)
If you ever need to stop or remove the container, you can do so with the following commands:

Stop the container:

bash
Copy code
docker stop mongo
Remove the container:

bash
Copy code
docker rm mongo
Final Notes
Always secure your MongoDB database and avoid exposing it to the public internet unless necessary. Consider using authentication and limiting access to trusted IPs only.
Use strong passwords and rotate them regularly.
Monitor your MongoDB instance and secure your environment as needed.


step 7 : 

to see if hte mongo is running and listneign on 27017 or not

docker logs < hashvalue > 
paste the hash value 

