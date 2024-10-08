# MyFirstPythonApp - Dockerized Flask Application

This project demonstrates how to build a simple Python web application using Flask, Docker, and Docker Compose. The project creates a containerized Python app that can be run locally or deployed to a cloud environment.

## Project Overview

This repository contains a basic Flask web application. The app simply returns "Hello, Docker!" when accessed via a web browser. Docker is used to containerize the application, making it easy to run in any environment.

### Technologies Used:
- **Python**: Programming language used for building the Flask application.
- **Flask**: A lightweight web framework for Python.
- **Docker**: Containerization tool used to build and run the application in isolated environments.
- **Docker Compose** (Optional): To orchestrate the application and its dependencies.

## Table of Contents

1. [Project Structure](#project-structure)
2. [Pre-requisites](#pre-requisites)
3. [Getting Started](#getting-started)
4. [Docker Commands](#docker-commands)
5. [Troubleshooting](#troubleshooting)
6. [References](#references)

## Project Structure

```bash
.
├── app.py              # Main Flask application
├── Dockerfile          # Instructions to build the Docker image
├── requirements.txt    # Python dependencies
└── README.md           # Project documentation (this file)
```

### File Descriptions:
- `app.py`: Contains the Flask application code.
- `Dockerfile`: Used by Docker to build a containerized version of the application.
- `requirements.txt`: Lists the dependencies required by the app (Flask and Werkzeug).

## Pre-requisites

Before you begin, ensure you have met the following requirements:

1. **Docker** installed on your machine.
   - [Install Docker](https://docs.docker.com/get-docker/)
   
2. **Python** installed (optional for local testing without Docker).
   - [Install Python](https://www.python.org/downloads/)

## Getting Started

### Step 1: Clone the Repository

```bash
git clone https://github.com/yourusername/myfirstpythonapp.git
cd myfirstpythonapp
```

### Step 2: Create the `Dockerfile`

Create a `Dockerfile` in your project root with the following content:

```Dockerfile
# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install the required packages
RUN pip install --no-cache-dir -r requirements.txt

# Expose the port the app runs on
EXPOSE 80

# Run the app
CMD ["python", "app.py"]
```

### Step 3: Create the Flask Application (`app.py`)

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
    return "Hello, Docker!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=80)
```

### Step 4: Create the `requirements.txt`

List the required Python dependencies:

```txt
Flask==2.0.3
Werkzeug==2.0.3
```

### Step 5: Build the Docker Image

Run the following command to build the Docker image:

```bash
docker build -t myfirstpythonapp .
```

### Step 6: Run the Application in a Docker Container

Once the image is built, you can run it using:

```bash
docker run -p 4000:80 myfirstpythonapp
```

Now, navigate to `http://localhost:4000` in your browser to see the app running!

## Docker Commands

### Build the Docker Image

```bash
docker build -t myfirstpythonapp .
```

### Run the Docker Container

```bash
docker run -p 4000:80 myfirstpythonapp
```

### Stop the Running Container

To stop the container, first find the container ID using:

```bash
docker ps
```

Then stop it using:

```bash
docker stop <container_id>
```

### Docker Compose (Optional)

You can use Docker Compose to simplify running multiple services, such as a database alongside your app. Create a `docker-compose.yml` file:

```yaml
version: '3'
services:
  app:
    build: .
    ports:
      - "4000:80"
```

To run the app using Docker Compose:

```bash
docker-compose up
```

## Troubleshooting

### Common Errors:
1. **`Dockerfile cannot be empty`**: Ensure that the `Dockerfile` is present in the project root directory and has valid content.
2. **`ImportError: cannot import name 'url_quote' from 'werkzeug.urls'`**: This is due to incompatibility between Flask and Werkzeug. Ensure you are using compatible versions (`Flask==2.0.3` and `Werkzeug==2.0.3`).

### Debugging Tips:
- Use `docker logs <container_id>` to view logs from your container.
- Use `docker exec -it <container_id> /bin/sh` to open a shell inside the running container for debugging.

## References

- [Docker Documentation](https://docs.docker.com/)
- [Flask Documentation](https://flask.palletsprojects.com/)
- [Python Official Website](https://www.python.org/)

