# AWS ElastiCache with Redis: Step-by-Step Guide

## Overview

Amazon ElastiCache is a fully managed in-memory caching service that supports Redis and Memcached. This guide focuses on using Redis with Amazon ElastiCache, providing an overview of Redis, its use cases, and step-by-step instructions on how to create a Redis cluster, configure security groups, and manage traffic.

## What is Redis?

Redis (Remote Dictionary Server) is an open-source, in-memory key-value data store that is used as a database, cache, and message broker. It supports various data structures such as strings, hashes, lists, sets, and more.

### Key Features of Redis

- **In-memory storage:** Redis stores data in memory, providing extremely low latency.
- **Persistence options:** You can choose to persist data on disk if needed.
- **Replication:** Redis supports master-slave replication for high availability.
- **Clustering:** Redis can be deployed in a cluster configuration, allowing data to be partitioned across multiple nodes.

## Step-by-Step: Setting Up ElastiCache with Redis

### 1. Creating an ElastiCache Redis Cluster

1. **Log in to AWS Management Console**:
   - Go to the [AWS Management Console](https://aws.amazon.com/console/).
   - Sign in with your credentials.

2. **Navigate to ElastiCache**:
   - In the AWS Management Console, type "ElastiCache" in the search bar and select it.
   - Click on "Create" to start setting up your cluster.

3. **Select Redis**:
   - Choose Redis as the caching engine.
   - Click "Next" to proceed.

4. **Cluster Configuration**:
   - **Name**: Enter a unique name for your cluster.
   - **Node Type**: Choose the instance type (e.g., `cache.t2.micro` for testing).
   - **Number of Replicas**: Decide how many replicas you need for high availability (0) FOR NOW.
   - **Subnet Group**: Select a subnet group or create a new one if needed.
   - **VPC**: Select the VPC where your Redis cluster will be deployed.

5. **Security Settings**:
   - **Security Groups**: Choose an existing security group or create a new one.
   - **Encryption**: Enable encryption at-rest and in-transit if required for your application.
   - **Access Control Lists (ACLs)**: Set up ACLs if you want to control access to specific commands or data within Redis.

6. **Review and Create**:
   - Review your settings.
   - Click "Create" to launch your Redis cluster.

### 2. Configuring Security Groups for Redis

1. **Access the Security Groups**:
   - In the AWS Management Console, go to "EC2".
   - Create a instance with Amazon Linux 2 AMI (HVM) - Kernel 5.10, SSD Volume Type
   - Click on "Security Groups".

2. **Create or Modify a Security Group**:
   - **Modify Security Group**: Select an existing security group and click on "Edit Inbound Rules".

3. **Set Inbound Rules**:
   - **Add Rule**:
     - **Type**: Select "Custom TCP Rule".
     - **Port Range**: Enter `6379`, the default port for Redis.
     - **Source**: Specify the IP range or security group that is allowed to connect.
   - **Save Rules**: Click "Save" to apply the rules.

4. **Attach the Security Group to the Redis Cluster**:
   - Go back to the ElastiCache console.
   - Select your Redis cluster.
   - Click on "Modify".
   - Attach the new or modified security group to your cluster.
   - Click "Apply Changes".

### 3.Connecting to an AWS EC2 Instance with MobaXterm and Installing Redis

## Step 1: Connect to Your EC2 Instance

1. **Launch MobaXterm**:
   - Open MobaXterm on your local machine.

2. **Start a New SSH Session**:
   - Click on "Session" in the top left corner.
   - Choose "SSH" from the options.
   - In the "Remote host" field, enter the public IP address of your EC2 instance.
   - In the "Specify username" field, enter `ec2-user`.
   - Click on "Advanced SSH settings" and select your `.pem` file (key pair) under "Use private key".

3. **Connect**:
   - Click "OK" to connect to your EC2 instance.
   - If prompted to save the session, you can choose to do so for easier access next time.

## Step 2: Installing Redis on the EC2 Instance

Once you are connected to your EC2 instance, execute the following commands in the MobaXterm terminal:

| **Command**                                                  | **Explanation**                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| sudo amazon-linux-extras install epel -y                     | Installs the Extra Packages for Enterprise Linux (EPEL) repository on an Amazon Linux instance. The `-y` flag automatically confirms the installation. |
| sudo yum install gcc jemalloc-devel openssl-devel tcl tcl-devel -y | Installs necessary tools and libraries, including the GNU Compiler Collection (`gcc`), memory allocator (`jemalloc`), OpenSSL libraries, and Tcl development libraries on your instance. |
| sudo wget http://download.redis.io/redis-stable.tar.gz       | Downloads the latest stable version of Redis from the official Redis website. |
| sudo tar xvzf redis-stable.tar.gz                            | Extracts the downloaded Redis archive file to your current directory. |
| cd redis-stable                                              | Navigates into the extracted Redis directory.                |
| sudo make                                                    | Compiles the Redis source code.                              |
| make BUILD_TLS=yes                                           | Compiles Redis with TLS (Transport Layer Security) support.  |

| **Command**                                                  | **Explanation**                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| cd src                                                       | Navigates into the `src` directory containing the compiled Redis binaries. |
| chmod a+x redis-cli                                          | Gives executable permission to the `redis-cli` binary.       |
| cp redis-cli /usr/bin/                                       | Copies the `redis-cli` binary to `/usr/bin/` for easy access from anywhere on the system. |
| redis-cli -h your-cluster-name.cache.amazonaws.com --tls -a YOURPASSWORD -p 6379 | Connects to your Redis cluster over TLS using the provided hostname, password, and port 6379. |


After running these commands, Redis will be installed on your EC2 instance.

# Redis Setup and Configuration

## Step 3: Continue with Redis Setup and Configuration

After installing Redis, you can continue with the setup by configuring Redis, starting the Redis server, and setting up security groups as mentioned in the previous steps of this guide.

### 1. Start the Redis Server

To start the Redis server, navigate to the directory where Redis was installed and use the following command:

```bash
src/redis-server
```

### 2. Set Up Security Groups

Return to the AWS Management Console and attach the necessary security groups as described earlier. Ensure that inbound and outbound rules are configured to allow access from trusted IP ranges or specific applications. You can view and manage these settings under the **EC2 Dashboard > Security Groups** section.

### 3. Manage Traffic and Access

To manage traffic and access to Redis, use Redis endpoints and follow best practices like scaling the Redis cluster and monitoring performance. Detailed configurations for traffic management and access control can be done using Redis configurations (`redis.conf`) and security group settings on AWS.

### 4. Monitoring and Maintenance

#### Monitoring Metrics

Key metrics such as CPU Utilization, Free Memory, and Network Traffic should be regularly monitored. AWS CloudWatch can be used for tracking these metrics.

#### Backups and Restores

Enable automated snapshots for periodic backups. Additionally, create manual snapshots before making major changes. You can manage and view backups under **Elasticache > Snapshots**. To restore from a snapshot, follow the restore process in the same section.

### Best Practices

- **Security**: Use VPCs and security groups to restrict access and avoid exposing Redis directly to the internet.
- **Persistence**: Enable RDB (Redis Database Backup) or AOF (Append-Only File) persistence for durability. You can manage these options using Redis configuration commands.
- **Scaling**: Regularly review your Redis workload and adjust your scaling strategy to match your needs.

### Verify Configurations in Redis

Once Redis is running, you can verify key configurations:

#### 1. Check Redis Server Status

Use the following command to verify that the Redis server is running and responsive:

```bash
redis-cli ping
```

Expected output: `PONG`

#### 2. Verify Redis Configuration Settings

To view the current configuration settings:

```bash
CONFIG GET *
```

This command displays all current configuration parameters.

#### 3. Verify Persistence Settings

To check the persistence settings like RDB and AOF, run the following commands:

```bash
CONFIG GET save
CONFIG GET appendonly
CONFIG GET dir
```

These settings determine how Redis saves data and the directory where it stores the data files.

---

For further Redis setup and configuration details, refer to the [Redis documentation](https://redis.io/documentation).
