

# **🐳 MySQL Docker Setup**  

![Docker Hub Repository](https://github.com/graheetphartyal23/Docker/blob/main/Contanerised%20MySQL/Screenshot%202025-03-28%20210906.png)

This repository contains a Docker setup for running a **MySQL container** with an initial database setup.  

---

## **📌 Features**  
✅ Pre-configured **MySQL Database** – Automatically sets up a MySQL instance.  
✅ **Database Initialization** – Runs `database.sql` on the first startup.  
✅ **Custom Port Mapping** – Runs MySQL on a user-defined port.  
✅ **Easy Setup & Deployment** – Simple commands to build and run.  

---

## **🛠️ Setup Instructions**  

### **✅ Step 1: Create the Project Directory**  
```bash
mkdir mysql-docker-setup
cd mysql-docker-setup
```

---

### **✅ Step 2: Create a `Dockerfile`**  
Create a `Dockerfile` and add the following content:  

```dockerfile
# Use the official MySQL image
FROM mysql:latest

# Set environment variables for MySQL
ENV MYSQL_ROOT_PASSWORD=root
ENV MYSQL_DATABASE=mydatabase
ENV MYSQL_USER=myuser
ENV MYSQL_PASSWORD=mypassword

# Copy initialization script
COPY database.sql /docker-entrypoint-initdb.d/
```

---

### **✅ Step 3: Create `database.sql` for Initial Setup**  
Create `database.sql` and add the following SQL commands:  

```sql
CREATE DATABASE IF NOT EXISTS mydatabase;
USE mydatabase;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE
);

INSERT INTO users (name, email) VALUES 
('Alice', 'alice@example.com'),
('Bob', 'bob@example.com');
```

---

### **✅ Step 4: Build the MySQL Docker Image**  
```bash
docker build -t mysql-container-new .
```

---

### **✅ Step 5: Run the MySQL Container on a Different Port (e.g., 3307)**  
```bash
docker run --name mysql-container-new -d -p 3307:3306 mysql-container-new
```
- `-d`: Runs in the background.  
- `-p 3307:3306`: Maps **MySQL’s port 3306** to local **port 3307**.  

---

### **✅ Step 6: Connect to MySQL Inside the Container**  
```bash
docker exec -it mysql-container-new mysql -u root -p
```
➡ **Enter password:** `root`  

---

### **✅ Step 7: Verify Database Initialization**  
Once inside MySQL, run these commands:  

```sql
SHOW DATABASES;
USE mydatabase;
SHOW TABLES;
SELECT * FROM users;
```

---

### **✅ Step 8: Stop and Remove the Container (Optional)**  
To stop MySQL:  
```bash
docker stop mysql-container-new
```  
To remove the container:  
```bash
docker rm mysql-container-new
```

---

## **🚀 Push Image to Docker Hub**  
To share the image on Docker Hub:  

### **✅ Step 1: Log in to Docker Hub**  
```bash
docker login
```
Enter your Docker Hub **username and password**.  

### **✅ Step 2: Tag the Image**  
```bash
docker tag mysql-container-new graheet/coa_1:latest
```

### **✅ Step 3: Push the Image**  
```bash
docker push graheet/coa_1:latest
```

### **✅ Step 4: Verify on Docker Hub**  
Go to: 🔗 **[Docker Hub Repository](https://hub.docker.com/r/graheet/coa_1)**  

---

## **📌 Project Structure**  
```
mysql-docker-setup/
│── database.sql     # SQL script for database initialization
│── Dockerfile       # Docker configuration file
│── README.md        # Project documentation
```






```bash
docker exec -it mysql-container-new mysql -u root
```

Then run:  
```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root';
FLUSH PRIVILEGES;
EXIT;
```
Restart the container and try again.  

---

## **👤 Author**  
**Graheet Phartyal**  
🔗 GitHub: [graheet](https://github.com/graheet)  

---

## **🚀 You Have Successfully Deployed MySQL in Docker!** 🎉  

