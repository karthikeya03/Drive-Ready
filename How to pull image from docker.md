# Docker and MongoDB Setup on EC2

# Docker Image and Container Analogy

- **Docker Image**: If you run an image, it becomes a container.
- **Analogy**: 
  - If the OS is on your pendrive, it's an **image** (just the stored form).
  - If it is running on your computer, then it's a **container** (the active, running form of the image).

## Steps

### 1. Creating an EC2 Instance

You first create an EC2 instance on AWS. This instance is a virtual machine that will act as your server.

### 2. Updating Packages

When you run `sudo yum update`, you're updating all the software packages on your EC2 instance. This ensures your system is up-to-date with the latest security patches and software updates.

To update all the software packages on your EC2 instance, run:

```bash
sudo yum update -y
```

This command updates the packages on your system and automatically answers "yes" to any prompts (`-y` flag).

### 3. Installing Docker

You install Docker, which is a platform that allows you to run applications in containers. Containers are lightweight, isolated environments for running applications, which makes it easy to deploy and manage software consistently.

To install Docker on your EC2 instance, run the following commands:

### 1. Install Docker:

```bash
sudo yum install docker -y
```

### 2. Start the Docker service:

```bash
sudo systemctl start docker
```

### 3. Enable Docker to start at boot:

```bash
sudo systemctl enable docker
```

### 4. Verify Docker is running:

```bash
sudo systemctl status docker
```

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
