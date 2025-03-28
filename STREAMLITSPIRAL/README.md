# Streamlit Spiral Visualization App with Docker

![Docker Hub Repository](https://github.com/graheetphartyal23/Docker/blob/main/STREAMLITSPIRAL/Screenshot%202025-02-20%20002538.png)
## Overview
Welcome to the **Streamlit Spiral Visualization App**! This project demonstrates an interactive Python application using Streamlit to visualize a spiral. You can customize the spiral’s properties using sliders and view real-time updates. The app is Dockerized for easy deployment.

##  Features
-  **Interactive Controls**: Adjust the number of points and turns in the spiral.
-  **Dynamic Visualization**: See real-time changes as you modify settings.
-  **Dockerized**: Ensures portability and consistency across environments.

##  Technologies Used
-  **Python 3**
-  **Streamlit** (for UI)
-  **Altair** (for visualization)
-  **Docker** (for containerization)
-  **Pandas** & **Numpy** (for data processing)

##  Prerequisites
Ensure you have the following installed:
- **Docker** (to build and run the app)
- **Git** (to clone the repository)

[Install Docker Here](https://docs.docker.com/get-docker/)

##  Setup and Installation
### Step 1: Clone the Repository
```sh
git clone https://github.com/JANHVI-18/DOCKER
cd Docker_Practices
```

### Step 2: Create a `requirements.txt` File
Ensure your directory includes a `requirements.txt` file with these dependencies:
```sh
streamlit
altair
pandas
numpy
```

### Step 3: Build the Docker Image
```sh
docker build -t streamlit-app .
```
Check if the image is built:
```sh
docker images
```

### Step 4: Run the Docker Container
```sh
docker run -p 8501:8501 streamlit-app
```

### Step 5: Access the App
Open your browser and go to:
```sh
http://localhost:8501
```

##  How It Works
-  **Sliders**: Adjust the number of points and turns.
-  **Real-Time Visualization**: Spiral updates dynamically.
-  **Mathematical Computation**: Uses polar coordinates and Altair charts for visualization.

##  Troubleshooting
- Check Docker logs for errors:
  ```sh
  docker logs <container_id>
  ```
- Ensure `requirements.txt` is correctly installed inside the Docker container.

##  Contributing
1.  Fork the repository.
2.  Create a new branch.
3.  Make your changes and commit them.
4.  Push to your fork.
5.  Open a pull request.

 **Happy Coding!** 

