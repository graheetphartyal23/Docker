
# 🚀 Docker Network Bridge Experiment  

This project demonstrates how to create and test a **custom Docker network** (`net-bridge`) to enable seamless inter-container communication. This helps in setting up **isolated, secure, and efficient** networking between containers.  

---

## 📌 Features  
✅ Create a **custom bridge network** for inter-container communication.  
✅ Run multiple containers and connect them to the same network.  
✅ Test connectivity via **ping** and **container name resolution**.  
✅ Use `docker inspect` to retrieve network details.  

---

## 🛠 Experiment Setup  

### **1️⃣ Create a Custom Docker Network** 🌐  
Run the following command to create a **custom bridge network**:  

```bash
docker network create --driver bridge --subnet 172.20.0.0/16 --ip-range 172.20.240.0/20 net-bridge
```
📌 If you get an error saying **"network with name net-bridge already exists"**, you can check existing networks using:  
```bash
docker network ls  
```
To remove an existing network before creating a new one, use:  
```bash
docker network rm net-bridge
```

---

### **2️⃣ Run Containers and Attach to the Network** 🖥️  

#### **Run a Database Container (Redis) 🛠️**
```bash
docker run -itd --net=net-bridge --name=cont_database redis
```

#### **Run a Server Container (BusyBox) 🖥️**
```bash
docker run -dit --name server-A --network net-bridge busybox
```

---

### **3️⃣ Inspect Network and Containers** 🔍  

#### **Check Network Details**  
```bash
docker network inspect net-bridge
```

#### **Check Container Details**  
```bash
docker inspect cont_database
```

#### **Get the Container IP Address**  
```bash
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' cont_database
```

---

### **4️⃣ Testing Connectivity** 🔗  

#### **Access the Shell of `server-A` Container**
```bash
docker exec -it server-A sh
```

#### **Ping the `cont_database` Container by IP**
```bash
ping 172.20.240.1  # Replace with the actual IP
```

#### **Ping the `cont_database` Container by Name**
```bash
ping cont_database
```

---

## 📌 Observations 📊  

✅ **Direct Communication Between Containers** – The custom bridge network allows direct communication between containers without exposing ports.  
✅ **IP Address Communication** – Containers can connect using their assigned IPs.  
✅ **Name Resolution** – Containers can be accessed using their names instead of IPs.  
✅ **Useful Debugging Tools** – Commands like `docker inspect` help in troubleshooting network issues.  

---

## 🏁 Conclusion 🎯  

This experiment showcases **Docker’s networking features**, enabling efficient and secure inter-container communication. Mastering Docker networking is **essential** for deploying scalable microservices and containerized applications. 🚀  

---

## 📸 Docker Network Connectivity Test 📈  

The following image shows successful communication between containers:  

![Docker Hub Repository](https://github.com/graheetphartyal23/Docker/blob/main/Docker%20network%20bridge/Screenshot%202025-03-28%20213339.png)

![Docker Hub Repository](https://github.com/graheetphartyal23/Docker/blob/main/Docker%20network%20bridge/Screenshot%202025-03-28%20213423.png)
---

## 🔗 Additional Resources  
- [Docker Networking Documentation](https://docs.docker.com/network/)  
- [Bridge Networks](https://docs.docker.com/network/bridge/)  

---
