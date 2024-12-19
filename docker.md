# Docker Notes

## What is Docker?
Docker is a platform that lets you build, ship, and run applications in lightweight, portable containers. Containers include everything needed to run an application, ensuring consistency across environments.

---

## Basic Docker Workflow
1. **Write Code**  
   - Write your application code and create a `Dockerfile` that defines how to package it.

2. **Build the Image**  
   - Use `docker build` to create a Docker image from your application and `Dockerfile`.

3. **Run the Container**  
   - Use `docker run` to create and run a container based on the image.

4. **Push to Docker Hub**  
   - Use `docker push` to upload your Docker image to a repository on Docker Hub.

5. **Deploy Anywhere**  
   - Pull and run the image on any machine with Docker installed.

---

## Detailed Process: Deploying an Application to Docker Hub

### Step 1: Install Docker

1. Download and install Docker Desktop for Windows:  
   [Docker Desktop](https://www.docker.com/products/docker-desktop)

2. Verify installation:

   ```bash
   docker --version
   ```

---

### Step 2: Create a Docker Hub Account

1. Visit [Docker Hub](https://hub.docker.com/).
2. Sign up for a free account.
3. Note your **username** and **password**.

---

### Step 3: Prepare a Simple Application

1. **Create a Project Folder**:   - Create a folder, e.g., `C:\my-docker-app`.

2. **Write Your Application**:   - Create a file named `app.py`:

   ```python
   print("Hello, Docker from Windows!")
   ```

3. **Create a Dockerfile**:   - In the same folder, create a file named `Dockerfile`:

   ```dockerfile
   # Use a lightweight Python image
   FROM python:3.9-slim
   
   # Copy the app file into the image
   COPY app.py /app/app.py
   
   # Set the working directory
   WORKDIR /app
   
   # Define the command to run the app
   CMD ["python", "app.py"]
   ```

---

### Step 4: Build the Docker Image

1. Open **Command Prompt** or **PowerShell**.

2. Navigate to your project folder:

   ```bash
   cd C:\my-docker-app
   ```

3. Build the Docker image:

   ```bash
   docker build -t my-first-app .
   ```

---

### Step 5: Run the Application

1. Start the app in a container:

   ```bash
   docker run my-first-app
   ```

2. Output:

   ```
   Hello, Docker from Windows!
   ```

---

### Step 6: Push to Docker Hub

1. Log in to Docker Hub:

   ```bash
   docker login
   ```

   Enter your Docker Hub username (**karthikeya0303**) and password.

2. Tag your image:

   ```bash
   docker tag my-first-app karthikeya0303/my-first-app
   ```

3. Push the image to Docker Hub:

   ```bash
   docker push karthikeya0303/my-first-app
   ```

---

### Step 7: Verify on Docker Hub

- Visit [Docker Hub](https://hub.docker.com/) and check your repository.

---

### Step 8: Run the App Anywhere

You can run your image on any machine with Docker:

```bash
docker pull karthikeya0303/my-first-app
docker run karthikeya0303/my-first-app
```

---

## Key Docker Commands

| Command                                | Description                                                  |
| -------------------------------------- | ------------------------------------------------------------ |
| `docker --version`                     | Verify Docker installation.                                  |
| `docker build -t <image-name> .`       | Build an image from the Dockerfile in the current directory. |
| `docker images`                        | List all Docker images.                                      |
| `docker run <image-name>`              | Run a container based on the specified image.                |
| `docker ps`                            | List running containers.                                     |
| `docker stop <container-id>`           | Stop a running container.                                    |
| `docker tag <image> <username>/<repo>` | Tag an image for pushing to Docker Hub.                      |
| `docker push <username>/<repo>`        | Push an image to Docker Hub.                                 |
| `docker pull <username>/<repo>`        | Pull an image from Docker Hub.                               |


Here is the content you requested as Markdown text with added notes:

# Simplified Docker Workflow

This is a simpler approach to test and deploy a basic Python application using Docker without complex build processes.

## Step 1: Use a Pre-Built Base Image

Instead of starting from scratch, use a base image with Python and minimal setup.

1. **Create the Docker Folder**  
   Create a folder named `docker` and inside it, create a file called `app.py` with the following content:

   ```python
   print("Hello, Docker from Windows!")
   ```

2. **Create the Dockerfile**  
   Inside the same folder, create a file named `Dockerfile` with the following content:

   ```dockerfile
   FROM python:3.9-slim
   COPY app.py /app/app.py
   WORKDIR /app
   CMD ["python", "app.py"]
   ```

## Step 2: Test Locally Without Dockerfile

You can test the Python script directly in a pre-built Python container without creating the `Dockerfile`.

Run the following command:

```bash
docker run --rm -v "%cd%":/app -w /app python:3.9-slim python app.py
```

**What this command does:**

- Pulls the `python:3.9-slim` image if it’s not already downloaded.
- Mounts your `docker` folder to the container.
- Runs `app.py` directly in the container.

## Step 3: Build the Docker Image

If Step 2 works, you can now build the Docker image.

Run the following command:

```bash
docker build -t my-first-app .
```

This command builds the image and tags it as `my-first-app`.

## Step 4: Run and Verify the Image

Once the image is built, run the container:

```bash
docker run my-first-app
```

**Expected Output:**

```
Hello, Docker from Windows!
```

## Alternative Without Building Dockerfile

If building a Dockerfile is still troublesome, you can push directly using Docker Hub's pre-built Python image.

1. **Run the container directly:**

   ```bash
   docker run --name hello-docker -it python:3.9-slim
   ```

2. **Inside the container, create the `app.py` file:**

   ```bash
   echo 'print("Hello, Docker from Python container!")' > app.py
   ```

3. **Run the Python script inside the container:**

   ```bash
   python app.py
   ```

---

