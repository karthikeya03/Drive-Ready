# Load Balancer and Kubernetes

## Load Balancer

### What is a Load Balancer?
A load balancer is a system that helps distribute incoming network traffic across multiple servers. Think of it like a traffic cop directing cars at a busy intersection. Without a load balancer, one server might get overwhelmed with too many requests, while others remain underused. The load balancer ensures that each server gets a fair share of traffic, which helps maintain the performance and reliability of the application.

![image](https://github.com/user-attachments/assets/40b1c578-83e7-43a3-a3f6-c85eba3ca05c)

### How Does it Work?
Imagine you have 5,000 users trying to access an application. Here’s how a load balancer handles this situation:
1. **Users** (2500)-> **Load Balancer** -> **EC2 Instance 1**
2. **Users** (2500)-> **Load Balancer** -> **EC2 Instance 2**

The load balancer sits between the users and the EC2 instances (servers) that run your application. It splits the traffic between these instances to ensure no single server becomes a bottleneck.

## Kubernetes

### What is Kubernetes?
Kubernetes (often abbreviated as K8s) is an open-source platform designed to manage and automate the deployment of containerized applications. Containers are a way to package your application and its dependencies into a single unit that can run consistently across different environments.

### Example
Let’s say you’re working with an e-commerce application like Ajio. This application might use Kubernetes to manage its various components:
- **User Interface**: One container might handle the user interface, providing the website or app that users interact with.
- **Backend Services**: Another container might handle the backend logic, such as processing orders or managing user accounts.

Kubernetes helps by:
1. **Deploying Containers**: Ensuring that the right number of containers are running.
2. **Scaling**: Automatically adding more containers if traffic increases.
3. **Managing Failures**: Restarting containers if they crash.

### Key Components
1. **Pods**: The smallest units in Kubernetes. A pod can contain one or more containers that share the same network and storage resources.
2. **Services**: These provide a stable way to access pods. They act as a bridge between the user and the application running in the pods.
3. **Deployments**: Manage the deployment and scaling of pods. They ensure that the right number of pods are running and handle updates.

## Docker

### What is Docker?
Docker is a platform that allows you to build, ship, and run applications inside containers. Containers package an application and everything it needs to run (such as libraries and dependencies) into a single unit. This makes it easier to deploy applications consistently across different environments.

### Docker Registry and Orchestration
Before Docker, AWS didn’t have specialized services for container management. Docker introduced:
- **Docker Registry**: A place to store Docker images so you can pull them when needed.
- **Docker Swarm**: A simple tool to orchestrate containers, managing their deployment and scaling.

## AWS Managed Services

### AWS Lambda
AWS Lambda is a serverless computing service. This means you don’t need to manage servers or infrastructure. You simply upload your code, and Lambda runs it automatically in response to events (like an image upload to S3).

**Example**: If a user uploads a file to S3, Lambda can automatically trigger a function to process that file.

### AWS Elastic Beanstalk (EBS)
Elastic Beanstalk is a Platform-as-a-Service (PaaS) that simplifies deploying and managing applications. You upload your code, and Elastic Beanstalk handles the deployment, scaling, and monitoring.

**Example**: If you have a web application, you can deploy it using Elastic Beanstalk, which will automatically handle things like load balancing and scaling.

### Serverless Applications
Serverless applications are those where you don’t have to worry about managing servers. AWS Lambda, API Gateway, and DynamoDB are examples of services that let you build serverless applications.

**Example**: Building a serverless API with Lambda and API Gateway allows you to create a REST API that responds to HTTP requests without managing the server infrastructure.

# **Creating a Load Balancer in AWS**

## **Step-by-Step Process**
This is what you're trying to build:

![AWS Load Balancer Diagram](https://github.com/user-attachments/assets/e54a83d2-40fa-4cb0-8f93-82acbe6c9222)

---

### **1. Launch a Virtual Private Cloud (VPC)**

1. **Sign in to AWS Management Console**
   - Go to the [AWS Management Console](https://aws.amazon.com/console/).

2. **Navigate to VPC Dashboard**
   - In the AWS Management Console, search for and select "VPC" to open the VPC Dashboard.

3. **Create a New VPC**
   - Click on "Create VPC."
   - **Enter VPC details:**
     - **Name tag:** Enter a descriptive name (e.g., `MyVPC`).
     - **IPv4 CIDR block:** Enter a CIDR block for the VPC, such as `10.0.0.0/16`.
     - **IPv6 CIDR block:** (Optional) You can choose to add IPv6 if needed.
     - **Tenancy:** Choose "Default" unless you need dedicated instances.
   - Click "Create VPC."

### **2. Create Two Subnets**

1. **Navigate to Subnets**
   - In the VPC Dashboard, click on "Subnets."

2. **Create the First Subnet**
   - Click "Create subnet."
   - **Enter subnet details:**
     - **Name tag:** Enter a descriptive name (e.g., `Subnet-1`).
     - **VPC:** Select the VPC you created.
     - **Availability Zone:** Choose an availability zone (e.g., `us-east-1a`).
     - **IPv4 CIDR block:** Enter a subnet CIDR block, such as `10.0.1.0/24`.
   - Click "Create subnet."

3. **Create the Second Subnet**
   - Click "Create subnet" again.
   - **Enter subnet details:**
     - **Name tag:** Enter a descriptive name (e.g., `Subnet-2`).
     - **VPC:** Select the VPC you created.
     - **Availability Zone:** Choose a different availability zone (e.g., `us-east-1b`).
     - **IPv4 CIDR block:** Enter a different subnet CIDR block, such as `10.0.2.0/24`.
   - Click "Create subnet."

### **3. Create a Routing Table Connected to Both Subnets**

1. **Navigate to Route Tables**
   - In the VPC Dashboard, click on "Route Tables."

2. **Create a New Route Table**
   - Click "Create route table."
   - **Enter route table details:**
     - **Name tag:** Enter a descriptive name (e.g., `MyRouteTable`).
     - **VPC:** Select the VPC you created.
   - Click "Create route table."

3. **Associate Subnets with the Route Table**
   - Select the newly created route table from the list.
   - Go to the "Subnet Associations" tab.
   - Click "Edit subnet associations."
   - Select both subnets (e.g., `Subnet-1` and `Subnet-2`).
   - Click "Save changes."

### **4. Launch Two Separate EC2 Instances**

1. **Navigate to EC2 Dashboard**
   - In the AWS Management Console, search for and select "EC2" to open the EC2 Dashboard.

2. **Launch the First EC2 Instance**
   - Click "Launch Instance."
   - **Choose an AMI:** Select an Amazon Machine Image (e.g., Amazon Linux 2).
   - **Choose an Instance Type:** Select an instance type (e.g., `t2.micro`).
   - **Configure Instance:** Ensure the instance is launched in one of the subnets (e.g., `Subnet-1`).
   - **Add Storage:** Configure storage as needed.
   - **Add Tags:** Add tags to help identify the instance (e.g., Name: `Instance-1`).
   - **Configure Security Group:** Choose or create a security group allowing necessary traffic.
   - **Review and Launch:** Review settings and click "Launch."
   - **Select a Key Pair:** Select an existing key pair or create a new one for SSH access.

3. **Launch the Second EC2 Instance**
   - Repeat the steps to launch another instance.
   - Ensure this instance is launched in the second subnet (e.g., `Subnet-2`).
   - Name this instance (e.g., `Instance-2`).

---

## **Creating a Load Balancer in AWS**

### **1. Navigate to Load Balancers**
1. **Login to AWS Management Console:** 
   - Open your web browser and log in to the [AWS Management Console](https://aws.amazon.com/console/).

2. **Access EC2 Dashboard:**
   - In the AWS Management Console, type “EC2” in the search bar at the top and select “EC2” from the dropdown list.

3. **Locate Load Balancers:**
   - In the EC2 Dashboard, look at the left sidebar and scroll down to find the “Load Balancing” section.
   - Click on “Load Balancers” under “Load Balancing.”

### **2. Create a New Load Balancer**
1. **Initiate Load Balancer Creation:**
   - Click the “Create Load Balancer” button at the top of the Load Balancers page.

2. **Choose Load Balancer Type:**
   - You’ll be presented with three options:
     - **Application Load Balancer (ALB):** Best for HTTP/HTTPS traffic and provides advanced routing features.
     - **Network Load Balancer (NLB):** Ideal for handling TCP/UDP traffic at high performance.
     - **Gateway Load Balancer:** Used for third-party virtual appliances.
   - **Choose "Application Load Balancer"** if you’re dealing with HTTP/HTTPS traffic.

3. **Configure Load Balancer Settings:**
   - **Name:** Enter a unique name for your load balancer (e.g., `MyLoadBalancer`).
   - **Scheme:** Select "internet-facing" if you want your load balancer to be accessible from the internet. Choose "internal" if it's only for private use within a VPC.
   - **IP Address Type:** Choose "ipv4" unless you need IPv6 support.
   - **Listeners:** A listener is a process that checks for connection requests. Add an HTTP listener on port 80 by default.

4. **Availability Zones:**
   - Select the VPC where your instances are running.
   - Choose at least two Availability Zones and associate them with subnets for high availability.

5. **Click "Next: Configure Security Settings"** to proceed.

### **3. Configure Security Settings**
1. **SSL/TLS Configuration:** 
   - Since you are configuring an HTTP listener (non-encrypted traffic), you can skip the SSL configuration step. If you were setting up an HTTPS listener, you'd need to configure SSL certificates here.

2. **Click "Next: Configure Security Groups"** to continue.

### **4. Configure Security Groups**
1. **Assign Security Groups:**
   - Security groups act as a virtual firewall for your instances.
   - **Choose an existing security group** or **create a new one**. Ensure that the security group allows incoming traffic on the listener port (e.g., HTTP port 80).

2. **Click "Next: Configure Routing"** to move forward.

### **5. Configure Routing**
1. **Target Group Configuration:**
   - A target group is a logical grouping of instances that your load balancer will route traffic to.
   - **Target Group Name:** Enter a name for the target group (e.g., `MyTargetGroup`).
   - **Target Type:** Select "Instance" to route traffic to EC2 instances.
   - **Protocol:** Choose the protocol for routing (e.g., HTTP).
   - **Port:** Enter the port number on which the target instances will receive traffic (e.g., port 80).

2. **Health Checks:**
   - Configure health checks to ensure that only healthy instances receive traffic.
   - You can leave the default settings or customize the health check path, protocol, and response timeout.

3. **Click "Next: Register Targets"** to continue.

### **6. Register Targets**
1. **Select EC2 Instances:**
   - On the Register Targets page, you'll see a list of your EC2 instances.
   - **Select the instances** you want to include in the target group (e.g., `Instance-1` and `Instance-2`).

2. **Add to Registered:**
   - After selecting the instances, click "Add to registered" to move them to the registered targets list.

3. **Click "Next: Review"** to proceed.

### **7. Review and Create**
1. **Review Configuration:**
   - On the Review page, review all your settings to ensure everything is configured correctly.

2. **Create Load Balancer:**
   - If everything looks good, click the “Create” button to launch the load balancer.
   - AWS will begin provisioning your load balancer, which might take a few minutes.

### **8. Verify and Test**

1. **Check Load Balancer Status:**
   - In the Load Balancers section, ensure that the status of the new load balancer is "active."

2. **Test the Load Balancer:**
   - Access the DNS name of the load balancer (provided in the description tab of the load balancer details).
   - Open a web browser and enter the DNS name to verify that it routes traffic correctly to your EC2 instances.

---

## **Best Practices**
1. **Monitoring and Alerts:** 
   - Set up CloudWatch alarms to monitor your load balancer's performance and automatically alert you if something goes wrong.

2. **Auto Scaling:** 
   - Consider setting up Auto Scaling groups to automatically adjust the number of instances behind your load balancer based on demand.

3. **Security:** 
   - Regularly review and update your security groups and IAM policies to follow the principle of least privilege.

---

