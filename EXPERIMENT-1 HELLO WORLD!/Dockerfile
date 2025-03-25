# Use an official Python runtime as base image
FROM python:3.9

# Set the working directory
WORKDIR /app

# Copy the current directory contents into the container
COPY . .

# Install dependencies
RUN pip install flask

# Expose the application's port
EXPOSE 5000

# Define the command to run the application
CMD ["python", "app.py"]
