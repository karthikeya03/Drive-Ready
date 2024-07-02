# SESSION 11: Connecting to VM Using Linux

## Key Protocols

### SSH (Secure Shell)
- **Purpose:** Securely connect to a remote machine
- **Port Number:** 22

### SFTP (Secure File Transfer Protocol)
- **Purpose:** Secure file transfer between client and server
- **Port Number:** 22

## Steps to Use SFTP
1. Select **SFTP**.
2. Add IP address and username.
3. Go to **Advanced Settings**.
4. Use a private key.
5. Drag and drop files to upload.

### Connecting and Uploading Files via SFTP
1. Connect using **SFTP**.
2. Use a private key.
3. Drag and drop files to upload.

## Creating a Webpage on a Linux Server

### Steps to Launch a Linux Server and Host a Webpage

#### 1. Launch Hardware
- Start a virtual machine (VM).

#### 2. Install OS
- Use **Amazon Linux**.

#### 3. Install Webserver Application

##### Update the Server
- Command: `sudo yum update`
- Response: `Nothing to do` (if no updates are needed)

##### Install Webserver
- Command: `sudo yum install httpd`
- Follow the prompts and select 'y' to install.

#### 4. Configure Security Group
- Add security rules to control inbound and outbound traffic.
- Example: Allow access to the web server only for specific users (like students in uniform).

#### 5. Enable HTTP Traffic
- **Port Number:** 80 (for HTTP protocol)
- **Steps:**
  1. Go to the security settings of the EC2 instance.
  2. Select **Security Groups**.
  3. Edit inbound rules.
  4. Add a rule:
     - **Type:** HTTP
     - **Source:** 0.0.0.0/0 (allows access from any IP address)

#### 6. Start the Web Server
- Command: `sudo systemctl start httpd`

#### 7. Deploy Your Webpage
- Navigate to the default web directory: `cd /usr/share/httpd/noindex/`
- Edit the `index.html` file: `sudo vim index.html`

### Additional Notes
- **Email Server:** Uses a different protocol (e.g., SMTP).
- **Video Content Server:** May use UDP.
- **Domain Name:** Purchase and configure as needed.

 ![steps](https://raw.github.com/karthikeya03/IMAGES/JustMain/11.1.png)

## Example: Apache Web Server on AWS EC2

### Steps

#### 1. Launch with Ubuntu
#### 2. Update Package Lists
- Command: `sudo apt-get update`

#### 3. Install Apache2
- Command: `sudo apt-get install apache2`

#### 4. Enable Port Number 80
- Edit inbound rules to allow traffic on port 80 (HTTP).

#### 5. Start Apache2
- Command: `sudo systemctl start apache2`

#### 6. Default Web Root Directory
- **Path:** `/var/www/html/`
- Navigate there: `cd /var/www/html/`
- Edit `index.html`: `sudo vim index.html`

### Removing Default Index File (Optional)
- Remove default `index.html`: `sudo rm index.html`

### Copy Website Template Files
- Command: `sudo cp -r ~/Desktop/website-templates-master/* /var/www/html/`

### Set Correct Permissions
- Commands:
  - `sudo chown -R www-data:www-data /var/www/html/`
  - `sudo chmod -R 755 /var/www/html/`

### Setting Up Virtual Hosts for Multiple Websites

#### 1. Create Directories for Each Website
- Commands:
  - `sudo mkdir /var/www/html/site1`
  - `sudo mkdir /var/www/html/site2`

#### 2. Copy Template Files to Each Directory
- Commands:
  - `sudo cp -r ~/Desktop/website-templates-master/template1/* /var/www/html/site1/`
  - `sudo cp -r ~/Desktop/website-templates-master/template2/* /var/www/html/site2/`

#### 3. Create Virtual Host Configuration Files
- **For site1:**
  - Command: `sudo nano /etc/apache2/sites-available/site1.conf`
  - Content:
    ```plaintext
    <VirtualHost *:80>
        ServerAdmin webmaster@localhost
        ServerName site1.example.com
        DocumentRoot /var/www/html/site1
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>
    ```

- **For site2:**
  - Command: `sudo nano /etc/apache2/sites-available/site2.conf`
  - Content:
    ```plaintext
    <VirtualHost *:80>
        ServerAdmin webmaster@localhost
        ServerName site2.example.com
        DocumentRoot /var/www/html/site2
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>
    ```

#### 4. Enable the Sites
- Commands:
  - `sudo a2ensite site1.conf`
  - `sudo a2ensite site2.conf`

#### 5. Restart Apache2
- Command: `sudo systemctl restart apache2`

### Accessing the Websites
- Make sure your `/etc/hosts` file (or DNS settings) points `site1.example.com` and `site2.example.com` to your server's IP address if you're testing locally.
- **Edit `/etc/hosts`:**
  - Command: `sudo nano /etc/hosts`
  - Add:
    ```plaintext
    127.0.0.1 site1.example.com
    127.0.0.1 site2.example.com
    ```

## Example: NGINX on CentOS/RHEL

### Steps

#### 1. Launch with CentOS/RHEL
#### 2. Update Package Lists
- Command: `sudo yum update`

#### 3. Install Nginx
- Command: `sudo yum install nginx`

#### 4. Enable Port Number 80
- Edit inbound rules to allow traffic on port 80 (HTTP).

#### 5. Start Nginx
- Command: `sudo systemctl start nginx`

#### 6. Enable Nginx
- Command: `sudo systemctl enable nginx`

#### 7. Restart Nginx
- Command: `sudo systemctl restart nginx`

#### 8. Set Permissions
- Command: `sudo chmod 777 /var/www/html`

#### 9. Launch SFTP
#### 10. Open the Designated Folder
#### 11. Copy the HTML

## Enabling Port Number 80 (IIS on Windows)

1. **Server Manager:**
   - Add roles (2)
   - **Server roles → IIS (Add)**
2. Go to system storage, inet, www, and paste the file

## Elastic IP

### Steps

1. Allocate public IP.
2. Associate public IP address.
3. Add the virtual machine.
4. Example: Elastic IP address `52.2.155.150` has been associated.

## Automation Scripts

### Script 1
**Description:** Automates web server setup and deployment.
**Steps:**
1. Switch to the root user.
2. Update package lists.
3. Install Apache web server.
4. Start Apache service.
5. Change permissions of the `/var/www/html` directory.
6. Remove the default `index.html` file.
7. Create a new `index.html` file.
8. Write "this is technical hub" into the new `index.html` file.
9. Start Apache service again to ensure changes take effect.

**Script:**
```bash
#!/bin/bash
sudo su
apt-get update -y
apt-get install apache2 -y
systemctl start apache2
chmod 777 /var/www/html
rm /var/www/html/index.html
touch /var/www/html/index.html
echo "this is technical hub" > /var/www/html/index.html
systemctl start apache2

# Step-by-Step Guide for Elastic IPs Using Scripts

## Step 1: Launch an EC2 Instance

1. **Log in to AWS Management Console**: Navigate to the AWS Management Console.
2. **Navigate to the EC2 Dashboard**: Go to the "EC2 Dashboard".
3. **Launch Instance**: Click the "Launch Instance" button.
4. **Select an AMI**: Choose an Amazon Machine Image (AMI), such as Amazon Linux 2 AMI.
5. **Choose Instance Type**: Select an instance type (e.g., t2.micro) and click "Next: Configure Instance Details".
6. **Configure Instance**: Set up your instance configuration and click "Next: Add Storage".
7. **Add Storage**: Configure the storage settings and click "Next: Add Tags".
8. **Add Tags**: Optionally add any tags and click "Next: Configure Security Group".
9. **Configure Security Group**: Create or select a security group that allows HTTP traffic on port 80.
10. **Review and Launch**: Review your instance configuration, click "Launch", select or create a key pair, and click "Launch Instances".

## Step 2: Connect to Your EC2 Instance

1. **Select Instance**: In the EC2 Dashboard, click "Instances".
2. **Connect**: Select your instance and click "Connect".
3. **Follow Instructions**: Follow the instructions to connect via SSH using your key pair.

## Step 3: Run the Script on Your EC2 Instance

1. **Execute Script**: Run the following script on your EC2 instance:
    ```bash
    #!/bin/bash
    sudo su
    chmod 777 /var/www/html
    rm /var/www/html/index.html
    touch /var/www/html/index.html
    echo "this is technical hub" > /var/www/html/index.html
    ```

This script will:
- Switch to the root user.
- Change permissions of the `/var/www/html` directory.
- Remove the default `index.html` file.
- Create a new `index.html` file.
- Write "this is technical hub" into the new `index.html` file.

