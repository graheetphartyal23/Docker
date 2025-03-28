
# **Microservices Architecture with Docker Swarm** ⚓️  

![Docker Hub Repository](https://github.com/graheetphartyal23/Docker/blob/main/Microservices%20Architecture%20using%20Docker%20Swarm/Screenshot%202025-03-28%20215350.png)

This project demonstrates how to deploy a **Microservices Architecture** using **Docker Swarm**, with an **API Gateway** and a **Backend Service**.

---

## **📌 Steps to Run the Project**  

### **1️⃣ Install Docker & Initialize Swarm**  
Ensure Docker is installed and running:  
```bash
docker --version
docker swarm init
```

### **2️⃣ Set Up Project Structure**  
Create directories for the services:  
```bash
mkdir microservices-docker-swarm && cd microservices-docker-swarm
mkdir backend-service api-gateway
```

### **3️⃣ Create Microservices Code**  
#### **Backend Service**  
- Create `backend.py` inside `backend-service/`  
- Create a `Dockerfile` for it  

#### **API Gateway**  
- Create `api_gateway.py` inside `api-gateway/`  
- Create a `Dockerfile` for it  

### **4️⃣ Build Docker Images**  
```bash
docker build -t backend-service ./backend-service
docker build -t api-gateway ./api-gateway
```

### **5️⃣ Deploy Services Using Docker Swarm**  
```bash
docker stack deploy -c docker-compose.yml my_microservices
```

### **6️⃣ Verify the Deployment**  
```bash
docker stack services my_microservices
docker ps
```

### **7️⃣ Access the API Gateway**  
Open your browser and go to:  
```
http://localhost:8080
```

Expected Output:  
```
API Gateway: rajput_tarakk
```

### **8️⃣ Scaling Services**  
Increase backend service replicas:  
```bash
docker service scale my_microservices_backend-service=5
```

### **9️⃣ Remove Services & Exit Swarm**  
```bash
docker stack rm my_microservices
docker swarm leave --force
```

---

## **📚 Resources**  
- [Docker Swarm Docs](https://docs.docker.com/engine/swarm/)  
- [Flask Docs](https://flask.palletsprojects.com/)  

---

🎉 **That's it! You've successfully deployed microservices using Docker Swarm!** 🚀
