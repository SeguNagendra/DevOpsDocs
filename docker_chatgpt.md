📌 1. What is Docker?

Docker is an open-source platform that lets you build, package, ship, and run applications inside containers.

A container is a lightweight, portable environment that bundles your application + dependencies.

Ensures consistency across development → testing → production.

Real-Life Example:
Think of Docker like shipping containers in cargo ships:

Containers isolate goods → no conflicts.

Docker isolates apps → no dependency issues.

📌 2. Why Use Docker?
Feature	Without Docker	With Docker
Environment Setup	Manual installation	Ready in seconds
Portability	Works only on some systems	Runs anywhere
Resource Usage	Heavy, uses VM per app	Lightweight containers
Deployment Speed	Minutes to hours	Few seconds
📌 3. Docker Architecture

Docker follows a client-server architecture.

Components

Docker Client (docker): Sends commands.

Docker Daemon: Runs in the background, manages containers & images.

Docker Images: Read-only templates for containers.

Docker Containers: Running instances of images.

Docker Volumes: Store persistent data.

Docker Networks: Enable container-to-container communication.

+---------------------------+
|     Docker Client        |
|   (docker commands)      |
+-----------+---------------+
            |
            v
+---------------------------+
|      Docker Daemon       |
| (Manages containers,     |
| images, networks, etc.)  |
+-----------+---------------+
            |
  -------------------------
  |       |       |       |
Container Container Container

📌 4. Docker Installation
Windows / Mac

Download Docker Desktop → https://www.docker.com/get-started

Install and start Docker Desktop.

Verify installation:

docker --version

Linux
sudo apt update
sudo apt install docker.io -y
docker --version

📌 5. Images vs Containers
Aspect	Docker Image	Docker Container
Definition	Blueprint/template	Running instance of an image
Modifiable	❌ No	✅ Yes
Size	Lightweight	Slightly larger
Example	nginx:latest	A running Nginx server

Example:

# Pull Nginx image
docker pull nginx

# Run a container from image
docker run -d -p 8080:80 nginx

📌 6. Essential Docker Commands
🔹 Image Commands
# List images
docker images

# Pull an image from Docker Hub
docker pull ubuntu

# Remove an image
docker rmi <image_id>

🔹 Container Commands
# Run a container
docker run -d -p 8080:80 nginx

# List running containers
docker ps

# List all containers (including stopped ones)
docker ps -a

# Stop a container
docker stop <container_id>

# Remove a container
docker rm <container_id>

# Access inside a running container
docker exec -it <container_id> /bin/bash

🔹 Volume & Network Commands
docker volume create mydata
docker volume ls
docker network ls

🔹 Cleanup Unused Resources
docker system prune -a

📌 7. Dockerfile Basics

A Dockerfile is a script with instructions to build a custom image.

Example Dockerfile:

# Use base image
FROM ubuntu:20.04

# Install dependencies
RUN apt-get update && apt-get install -y python3

# Copy app files
COPY app.py /app/app.py

# Set working directory
WORKDIR /app

# Set default command
CMD ["python3", "app.py"]


Build & Run:

docker build -t myapp .
docker run -d -p 5000:5000 myapp

# 🐳 Docker Components – Explained Simply

Docker has 5 main components that work together to build, run, and manage containers:

📌 1. Docker Client (Command-Line Interface)

The Docker Client is what you use to interact with Docker.

You run commands like:

docker run nginx
docker ps


The client sends these commands to the Docker Daemon for execution.

Example:
If you type:

docker run nginx


The Docker Client tells the Daemon:

“Hey! Please create a container using the Nginx image.”

📌 2. Docker Daemon (dockerd)

The Docker Daemon is the brain of Docker 🧠.

It listens for commands from the client and does the real work:

Builds images

Runs containers

Manages networks and volumes

Runs in the background on your machine.

Think of it like:

You = Customer (Docker Client)

Daemon = Chef (actually prepares the dish — container)

📌 3. Docker Images

An image is like a template or recipe for a container.

It has everything your app needs:

Code

Runtime

Libraries

Configurations

Images are read-only → they cannot be modified directly.

Example:

The nginx image = Contains an already configured Nginx web server.

If you run:

docker pull nginx


It downloads the image from Docker Hub.

📌 4. Docker Containers

A container is a running instance of an image.

When you run an image, Docker creates a container from it.

Containers are:

Lightweight

Isolated (no conflict with other containers)

Portable (can run anywhere)

Example:

docker run -d -p 8080:80 nginx


Uses the nginx image.

Creates a container.

Runs a web server on http://localhost:8080
.

📌 5. Docker Registry (Docker Hub)

A Docker Registry stores Docker images.

By default, Docker uses Docker Hub (public registry).

You can:

Pull images → Download existing images.

Push images → Upload your own custom images.

Example:

docker pull ubuntu        # Download Ubuntu image
docker push myrepo/myapp  # Upload your own image

📌 How They Work Together

Here’s the step-by-step workflow when you run:

docker run nginx


Client → You type the command.

Daemon → Receives the request.

Registry → If the image isn’t available locally, Docker downloads it from Docker Hub.

Image → Uses the downloaded image as a base.

Container → Creates and starts a running container.

🔹 Docker Components in a Simple Diagram
        +---------------------------+
        |      Docker Client       |
        | (You run docker commands)|
        +------------+------------+
                     |
                     v
        +---------------------------+
        |     Docker Daemon        |
        | (Manages images & cont.) |
        +------------+------------+
                     |
         ----------------------------
         |                          |
         v                          v
+----------------+       +-----------------+
| Docker Images  |       | Docker Registry |
| (Templates)    |<----->| (Docker Hub)    |
+----------------+       +-----------------+
         |
         v
+----------------+
| Docker         |
| Containers     |
| (Running Apps) |
+----------------+

Summary of Docker Components
Component	Role	Example
Docker Client	Sends commands to Docker	docker run nginx
Docker Daemon	Executes commands & manages objects	Starts a container
Docker Images	Templates used to create containers	nginx:latest
Docker Containers	Running instances of images	Running Nginx web server
Docker Registry	Stores & shares images	Docker Hub


# 🐳 🐳 Docker Images & Containers Commands Cheat Sheet

This cheat sheet contains all important Docker commands related to images and containers with explanations and examples.

📌 1. Docker Image Commands

Docker images are templates used to create containers. Below are the most commonly used image-related commands.

🔹 1.1 List Docker Images
docker images


Description: Shows all images stored locally.

🔹 1.2 Pull an Image from Docker Hub
docker pull <image_name>


Example:

docker pull nginx


Downloads the nginx image from Docker Hub.

🔹 1.3 Search for an Image on Docker Hub
docker search <image_name>


Example:

docker search ubuntu


Displays available Ubuntu images from Docker Hub.

🔹 1.4 Build an Image from a Dockerfile
docker build -t <image_name> .


Example:

docker build -t myapp .


Builds an image named myapp using the Dockerfile in the current directory.

🔹 1.5 Tag an Image
docker tag <image_id> <repository>/<image_name>:<tag>


Example:

docker tag 123abc myrepo/myapp:v1


Gives a custom name and version to an image.

🔹 1.6 Push an Image to Docker Hub
docker push <repository>/<image_name>:<tag>


Example:

docker push myrepo/myapp:v1


Uploads your image to Docker Hub.

🔹 1.7 Inspect an Image
docker inspect <image_id>


Displays detailed metadata about an image.

🔹 1.8 Remove an Image
docker rmi <image_id>


Example:

docker rmi nginx


Deletes the nginx image from your system.

🔹 1.9 Remove Unused (Dangling) Images
docker image prune


Removes unused images that are not associated with any container.

🔹 1.10 Save an Image to a Tar File
docker save -o <file_name>.tar <image_name>


Example:

docker save -o myapp.tar myapp:latest


Saves the image into a .tar file.

🔹 1.11 Load an Image from a Tar File
docker load -i <file_name>.tar


Example:

docker load -i myapp.tar


Loads the image back into Docker.

📌 2. Docker Container Commands

Containers are running instances of Docker images.
Here are the most commonly used container-related commands.

🔹 2.1 Run a Container
docker run <image_name>


Example:

docker run ubuntu


Runs a container from the Ubuntu image.

🔹 2.2 Run a Container in Detached Mode
docker run -d <image_name>


Example:

docker run -d nginx


Runs the container in the background.

🔹 2.3 Run a Container with Port Mapping
docker run -d -p <host_port>:<container_port> <image_name>


Example:

docker run -d -p 8080:80 nginx


Maps host port 8080 to container port 80.

🔹 2.4 Run a Container with a Custom Name
docker run --name <container_name> <image_name>


Example:

docker run --name myweb nginx


Creates a container named myweb.

🔹 2.5 List Running Containers
docker ps


Shows active containers.

🔹 2.6 List All Containers (Including Stopped)
docker ps -a


Displays all containers.

🔹 2.7 Start a Stopped Container
docker start <container_id>


Starts a container that was previously stopped.

🔹 2.8 Stop a Running Container
docker stop <container_id>


Stops a running container.

🔹 2.9 Restart a Container
docker restart <container_id>


Restarts a container.

🔹 2.10 Remove a Container
docker rm <container_id>


Example:

docker rm myweb


Deletes the container named myweb.

🔹 2.11 Remove All Stopped Containers
docker container prune


Removes all inactive containers.

🔹 2.12 View Logs of a Container
docker logs <container_id>


Example:

docker logs myweb


Displays container logs.

🔹 2.13 Access a Container’s Shell
docker exec -it <container_id> /bin/bash


Example:

docker exec -it myweb /bin/bash


Gives you an interactive terminal inside the container.

🔹 2.14 Copy Files Between Host and Container

From Host → Container:

docker cp file.txt <container_id>:/app/


From Container → Host:

docker cp <container_id>:/app/file.txt .

🔹 2.15 Inspect a Container
docker inspect <container_id>


Shows detailed information about a container.

🔹 2.16 Check Resource Usage
docker stats


Displays CPU, memory, and network usage of running containers.

🔹 2.17 Rename a Container
docker rename <old_name> <new_name>


Example:

docker rename myweb myserver


Renames container myweb to myserver.

🔹 2.18 Pause & Unpause a Container
docker pause <container_id>
docker unpause <container_id>


Temporarily suspends and resumes a container.

📌 3. Useful Combined Commands
Command	Description
docker stop $(docker ps -aq)	Stop all running containers
docker rm $(docker ps -aq)	Remove all containers
docker rmi $(docker images -q)	Remove all images
docker system prune -a	Remove all unused containers, images, and networks
# 📌 Summary Table
# **🐳 Docker Images & Containers – Summary Table**

| **Command**        | **Description**             | **Example**                          |
|---------------------|----------------------------|-------------------------------------|
| `docker images`    | List local images          | `docker images`                     |
| `docker pull`      | Download an image         | `docker pull nginx`                 |
| `docker rmi`       | Remove an image          | `docker rmi nginx`                  |
| `docker run`       | Run a container         | `docker run nginx`                  |
| `docker ps`        | List running containers | `docker ps`                         |
| `docker ps -a`     | List all containers    | `docker ps -a`                      |
| `docker stop`      | Stop a container     | `docker stop myweb`                 |
| `docker rm`        | Remove a container   | `docker rm myweb`                   |
| `docker logs`      | View container logs | `docker logs myweb`                 |
| `docker exec`      | Open container shell | `docker exec -it myweb /bin/bash`   |

# **🐳 Docker Volumes – Complete Guide**

## **📌 What is a Docker Volume?**
A **Docker volume** is a **persistent storage mechanism** used by containers.  
By default, when a container is removed, **all its data is lost**.  
Volumes help store data **outside the container’s writable layer** so that the data **persists** even if the container is deleted or restarted.

### **🔹 Why Use Volumes?**
- Persist application data.
- Share data between multiple containers.
- Backup and restore container data.
- Separate application storage from container lifecycle.
- Improve performance compared to bind mounts.

---

## **📌 Types of Docker Volumes**

Docker supports **three main types** of volumes:

### **1. Named Volumes**
- Created and managed by Docker.
- Data is stored inside Docker’s storage path (`/var/lib/docker/volumes/`).
- Easiest and most common way to manage persistent data.

**Example:**
```bash
docker volume create myvolume
docker run -d -v myvolume:/app/data nginx


