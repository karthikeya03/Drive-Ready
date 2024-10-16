# Docker and MongoDB Setup on EC2

# Docker Image and Container Analogy

- **Docker Image**: If you run an image, it becomes a container.
- **Analogy**: 
  - If the OS is on your pendrive, it's an **image** (just the stored form).
  - If it is running on your computer, then it's a **container** (the active, running form of the image).

## Steps

### 1. Creating an EC2 Instance

You first create an EC2 instance on AWS. This instance is a virtual machine that will act as your server.

### 2. Updating Packages and installing Docker

# Updating Packages and Installing Docker on Ubuntu EC2 Instance

## 1. Updating Packages

To update all the software packages on your EC2 instance, run the following commands:

```bash
sudo apt-get update -y
sudo apt-get upgrade -y
```

This updates the package list and installs the latest versions of the packages.

---

### 3. Installing Docker

To install Docker on an Ubuntu EC2 instance, follow these steps:

### 3.1 Install Prerequisites:

Run the following command to install the required packages:

```bash
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common -y
```

### 3.2 Add Docker's Official GPG Key:

To add Docker’s official GPG key, run the following command:

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

### 3.3 Add Docker's Official Repository:

Run the following command to add Docker's official repository to your sources list:

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### 3.4 Update the Package Database:

Update the package database again with the following command:

```bash
sudo apt-get update
```

### 3.5 Install Docker:

Run the following command to install Docker:

```bash
sudo apt-get install docker-ce -y
```

### 3.6 Start the Docker Service:

Start the Docker service using the following command:

```bash
sudo systemctl start docker
```

### 3.7 Enable Docker to Start at Boot:

To ensure Docker starts automatically when the system boots, run:

```bash
sudo systemctl enable docker
```

### 3.8 Verify Docker is Running:

Check the status of the Docker service with:

```bash
sudo systemctl status docker
```

---
This will display the status of the Docker service.

### 4. Docker Network Management

- `docker network ls`: Lists the networks available in Docker. Docker networks allow containers to communicate with each other, and they isolate different sets of containers.

- `docker network create mongo-network`: Creates a new network in Docker named `mongo-network`. This is an isolated network where your MongoDB and other containers can communicate with each other.

### 5. Pulling the MongoDB Image

- `docker pull mongo`: Pulls the MongoDB image from Docker Hub (the image repository). This is a pre-packaged version of MongoDB, which is a NoSQL database.

### 6. Configuring MongoDB

- `docker run -d -p 27017:27017 --name mongo --net mongo-network -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=pass mongo`: 

This command starts a MongoDB container and does the following:

- **`-d`**: Runs the container in detached mode (in the background).
- **`-p 27017:27017`**: Maps the port `27017` of your EC2 instance to port `27017` inside the container. MongoDB uses port `27017` by default.
- **`--name mongo`**: Names the container `mongo`.
- **`--net mongo-network`**: Connects the container to the `mongo-network` Docker network.
- **`-e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=pass`**: These environment variables set the root username (`admin`) and password (`pass`) for MongoDB.

### 7. Enabling Port 27017 in EC2 Security Groups

To allow external access to MongoDB, you need to open port `27017` in your EC2 instance's security group. This step ensures that your MongoDB instance can be accessed from outside (like from a browser or another machine).

### 8. Viewing MongoDB Logs

- `docker logs <container_id>`: This command shows the logs for your MongoDB container. The container ID will be something like `2e45f5fc835a`. This is useful for troubleshooting or ensuring that MongoDB started correctly.

### 9. Accessing MongoDB via Browser

- `<public-ip>:27017`: If you visit this URL in your browser (where `<public-ip>` is the public IP address of your EC2 instance), it tries to connect to MongoDB. However, since MongoDB is a database, it doesn't have a web interface directly—so you won't see much in the browser at this step.

### 10. Pulling the Mongo Express Image

- `docker pull mongo-express`: Pulls the `mongo-express` image from Docker Hub. Mongo Express is a web-based administrative interface for MongoDB, allowing you to interact with MongoDB via a web UI.

### 11. Enabling Port 8081 in EC2 Security Groups

- You need to enable port `8081` in your EC2 security group to allow access to Mongo Express via the web interface.

### 12. Running Mongo Express

- `docker run -d -p 8081:8081 --name mongo-express --net mongo-network -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=pass -e ME_CONFIG_MONGODB_SERVER=mongo mongo-express`:

This command starts the Mongo Express container and does the following:

- **`-d`**: Runs Mongo Express in detached mode.
- **`-p 8081:8081`**: Maps port `8081` of your EC2 instance to port `8081` inside the container (Mongo Express’s web interface uses port 8081).
- **`--name mongo-express`**: Names the container `mongo-express`.
- **`--net mongo-network`**: Connects the Mongo Express container to the `mongo-network`, so it can communicate with the MongoDB container.
- **`-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=pass -e ME_CONFIG_MONGODB_SERVER=mongo`**: These environment variables tell Mongo Express to use the `admin` username and `pass` password to connect to the MongoDB server.

### 13. Viewing Mongo Express Logs

- `docker logs <container_id>`: This shows the logs of the Mongo Express container to check for any issues during startup.

### 14. Accessing Mongo Express Web Interface

- `<public-ip>:8081`: If you visit this URL in your browser (where `<public-ip>` is the public IP of your EC2 instance), you should see the Mongo Express web interface, where you can manage your MongoDB database.

### Summary:

- You're setting up MongoDB and Mongo Express inside Docker containers on your EC2 instance.
- MongoDB is the database, and you're configuring it to run inside Docker.
- Mongo Express is a web-based interface for managing MongoDB.
- You're connecting these containers via a Docker network and opening the necessary ports in your EC2 instance's security groups so you can access the services from outside.
