# Python Logging Application with Docker

![Docker Hub Repository](https://github.com/graheetphartyal23/Docker/blob/main/Python%20Logging/Screenshot%202025-02-20%20013956.png)

## Overview
This project demonstrates a simple Python application that logs messages continuously to a file while running inside a Docker container. The logs are stored in a persistent Docker volume.

## Prerequisites
- Install [Docker](https://www.docker.com/get-started)

## Project Structure
```
.
├── app.py            # Python script for logging
└── Dockerfile        # Dockerfile to containerize the application
```

## Step 1: Create the Python Application
Create a file named `app.py` with the following content:

```python
import time

log_file = "/data/app.log"
with open(log_file, "a") as file:
    while True:
        file.write(f"Logging entry at {time.ctime()}\n")
        file.flush()
        time.sleep(5)
```
This script logs messages every 5 seconds to `/data/app.log`.

## Step 2: Create a Dockerfile
Create a `Dockerfile` to containerize the application:

```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY app.py /app/app.py
CMD ["python", "app.py"]
```

## Step 3: Build and Run the Docker Container
### Build the Image
```sh
docker build -t python-log-app .
```
### Run the Container with a Volume
```sh
docker run -d -v log-data:/data python-log-app
```
This ensures logs are stored in the `log-data` volume.

## Step 4: Check Logs
### View Running Containers
```sh
docker ps
```
### View Logs in Real-Time
```sh
docker logs <container_id>
```
### Access Log File Inside the Container
```sh
docker exec -it <container_id> cat /data/app.log
```

## Cleanup
### Stop and Remove the Container
```sh
docker stop <container_id>
docker rm <container_id>
```
### Remove the Docker Image (Optional)
```sh
docker rmi python-log-app
```
### Remove the Volume (Optional)
```sh
docker volume rm log-data
```

## Conclusion
This setup allows continuous logging inside a Docker container with persistent storage. 🚀

