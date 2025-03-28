# 🌍🚀 Hello World in Docker

This guide will walk you through deploying a simple **Hello World!** application in Python using Docker. We'll create a Dockerfile, build the Docker image, and run it as a container.

## 🛠️ Prerequisites
Before you begin, make sure you have:
- **Docker** installed on your system. [Download Docker](https://www.docker.com/)
- **Python 3** installed. Verify by running:
  ```sh
  python3 --version
  ```

## 🚀 Steps to Deploy

### 1️⃣ Create `app.py`
Create a Python script named `app.py`:
```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello World! 👋'

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

### 2️⃣ Create `Dockerfile`
Create a `Dockerfile` with the following content:
```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY . /app
RUN pip install --no-cache-dir -r requirements.txt
EXPOSE 5000
ENV FLASK_APP=app.py
CMD ["flask", "run", "--host=0.0.0.0"]
```

### 3️⃣ Create `requirements.txt`
List dependencies in `requirements.txt`:
```
flask
```

### 4️⃣ Build the Docker Image 🏗️
Run the following command in your project directory:
```sh
docker build -t hello-world-docker .
```

### 5️⃣ Run the Docker Container 🚢
Start the container:
```sh
docker run -p 5000:5000 hello-world-docker
```

### 6️⃣ Access the Application 🌍
Visit:
```
http://localhost:5000
```
You should see **Hello World! 👋**

### 7️⃣ Stop the Container 🛑
To stop the container:
```sh
docker ps  # Find the container ID
docker stop <container_id>
```

## 🧹 Clean Up
To remove the container and image:
```sh
docker rm <container_id>
docker rmi hello-world-docker
```

## 🔗 Repository
Find the full project on GitHub: [Hello World Docker](https://github.com/graheetphartyal23/Docker)

## 🎉 Conclusion
You've successfully deployed a **Hello World!** app using Python and Docker. Expand on this to build more complex applications!

Happy Dockerizing! 🚀🐳

