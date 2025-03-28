# Streamlit App with PostgreSQL using Docker
![Docker Hub Repository](https://github.com/graheetphartyal23/Docker/blob/main/Postgres%20%26%20streamlit/Screenshot%202025-02-20%20121616.png)

This project demonstrates how to set up a Streamlit application that connects to a PostgreSQL database using Docker. You'll create a custom Docker network, launch a PostgreSQL container, insert sample data, and deploy a Streamlit app to visualize the data.

## Prerequisites
- **Docker** installed on your system
- **Basic knowledge** of Docker, PostgreSQL, and Python

## Project Structure
```
.
├── Dockerfile      # Streamlit App Dockerfile
├── stream.py       # Streamlit application
└── README.md       # Project documentation
```

## Steps to Deploy

### 1️⃣ Create a Docker Network
Run the following command to create a custom network for communication between containers:
```sh
docker network create my_network
```

### 2️⃣ Start PostgreSQL Container
Launch a PostgreSQL container with a database:
```sh
docker run -d \
  --name my_postgres \
  --network my_network \
  -e POSTGRES_USER=admin \
  -e POSTGRES_PASSWORD=adminpassword \
  -e POSTGRES_DB=mydb \
  -p 5432:5432 \
  postgres
```

### 3️⃣ Insert Sample Data
Access PostgreSQL and add data:
```sh
docker exec -it my_postgres psql -U admin -d mydb
```
Then, run the following SQL commands:
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE
);

INSERT INTO users (name, email) VALUES
('Alice Johnson', 'alice@example.com'),
('Bob Smith', 'bob@example.com'),
('Charlie Brown', 'charlie@example.com');

SELECT * FROM users;
```
Exit using `\q`.

### 4️⃣ Create Streamlit App
Create a `stream.py` file with the following:
```python
import streamlit as st
import psycopg2

def get_db_connection():
    return psycopg2.connect(
        dbname="mydb",
        user="admin",
        password="adminpassword",
        host="my_postgres",
        port="5432"
    )

st.title("Streamlit App with PostgreSQL")

try:
    conn = get_db_connection()
    cur = conn.cursor()
    cur.execute("SELECT * FROM users;")
    rows = cur.fetchall()
    
    st.write("### User Data from PostgreSQL")
    for row in rows:
        st.write(f"**ID:** {row[0]} | **Name:** {row[1]} | **Email:** {row[2]}")
    
    cur.close()
    conn.close()
except Exception as e:
    st.error(f"Error: {e}")
```

### 5️⃣ Create Dockerfile for Streamlit
```Dockerfile
FROM python:3.9
WORKDIR /app
COPY . .
RUN pip install --no-cache-dir streamlit psycopg2
EXPOSE 8501
CMD ["streamlit", "run", "stream.py", "--server.port=8501", "--server.address=0.0.0.0"]
```

### 6️⃣ Build and Run Streamlit App
Build the Docker image:
```sh
docker build -t my_streamlit_app .
```

Run the Streamlit container:
```sh
docker run -d \
  --name streamlit_app \
  --network my_network \
  -p 8501:8501 \
  my_streamlit_app
```

### 7️⃣ View the Application
Open your browser and go to:
```
http://localhost:8501
```
You should see the user data displayed from the PostgreSQL database.

## Cleanup 🧹
To stop and remove the containers and network:
```sh
docker stop my_postgres streamlit_app
```
```sh
docker rm my_postgres streamlit_app
```
```sh
docker network rm my_network
```

## License
This project is licensed under the **MIT License**.

🚀 Happy Coding with Docker, Streamlit, and PostgreSQL! 🎉

