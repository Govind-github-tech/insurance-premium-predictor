# Insurance Premium Predictor

An end-to-end Machine Learning application that predicts insurance premiums based on user-provided personal and health-related information.

The project uses a **Random Forest** machine learning model exposed through a **FastAPI** backend. The backend is containerized using **Docker**, published to **Docker Hub**, and deployed on an **AWS EC2** instance.

---

## 🚀 Project Overview

The Insurance Premium Predictor takes user input, processes the data, and uses a trained Machine Learning model to predict the insurance premium.

### Application Flow

```text
User Input
    │
    ▼
Streamlit Frontend
    │
    ▼
FastAPI Backend
    │
    ▼
Data Preprocessing
    │
    ▼
Random Forest Model
    │
    ▼
Premium Prediction
    │
    ▼
Prediction Result
```

### Deployment Flow

```text
Local Development
       │
       ▼
   Dockerfile
       │
       ▼
 Docker Image
       │
       ▼
  Docker Hub
       │
       ▼
   AWS EC2
       │
       ▼
Docker Container
       │
       ▼
 FastAPI API
       │
       ▼
Public API Endpoint
```

---

## ✨ Features

- Insurance premium prediction using Machine Learning
- Random Forest regression model
- Data preprocessing and feature handling
- FastAPI REST API
- Streamlit frontend
- Dockerized FastAPI application
- Docker Hub image deployment
- AWS EC2 deployment
- Swagger API documentation
- API-based prediction

---

## 🛠️ Tech Stack

### Machine Learning

- Python
- Pandas
- NumPy
- Scikit-learn
- Random Forest

### Backend

- FastAPI
- Uvicorn
- REST API

### Frontend

- Streamlit

### Deployment

- Docker
- Docker Hub
- AWS EC2

---

## 📁 Project Structure

```text
insurance-premium-predictor/
│
├── app/
│   ├── main.py
│   └── ...
│
├── model/
│   └── ...
│
├── frontend/
│   └── ...
│
├── requirements.txt
├── Dockerfile
├── README.md
└── ...
```

> The exact project structure may vary depending on the implementation.

---

# ⚙️ Local Setup

## Prerequisites

Make sure the following are installed:

- Python 3.x
- Git
- Docker
- Docker Hub account

---

# 🐳 Docker Setup

## Step 1 — Install Docker

Install Docker Desktop on your local machine.

After installation, verify that Docker is installed correctly:

```bash
docker --version
```

---

## Step 2 — Create a Docker Hub Account

Create an account on Docker Hub if you do not already have one.

You will need your Docker Hub username to build and push the Docker image.

Throughout this README, the Docker Hub username is represented by:

```text
<DOCKER_USERNAME>
```

Replace `<DOCKER_USERNAME>` with your actual Docker Hub username.

---

## Step 3 — Create a Dockerfile

Create a file named:

```text
Dockerfile
```

in the root directory of the project.

Example Dockerfile:

```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8000

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
```

> Update the `CMD` path if your FastAPI application's entry point is different.

---

# 🏗️ Build the Docker Image

## Step 4 — Build the Docker Image

Open a terminal in the project root directory and run:

```bash
docker build -t <DOCKER_USERNAME>/insurance-premium-api .
```

This command:

- Builds the Docker image
- Uses the `Dockerfile`
- Tags the image with your Docker Hub username
- Creates the image named `insurance-premium-api`

Verify that the image was created:

```bash
docker images
```

You should see an image similar to:

```text
<DOCKER_USERNAME>/insurance-premium-api
```

---

# 🔐 Docker Hub

## Step 5 — Login to Docker Hub

Run:

```bash
docker login
```

Enter your Docker Hub username and password when prompted.

If the login is successful, Docker will display a successful authentication message.

---

## Step 6 — Push the Image to Docker Hub

Push the Docker image to Docker Hub:

```bash
docker push <DOCKER_USERNAME>/insurance-premium-api
```

The image will now be available in your Docker Hub repository.

---

# 📥 Pull the Docker Image

## Step 7 — Pull the Image

The Docker image can be downloaded from Docker Hub using:

```bash
docker pull <DOCKER_USERNAME>/insurance-premium-api:latest
```

This command is useful when deploying the application on another machine, such as an AWS EC2 instance.

---

# ▶️ Run the Docker Image Locally

## Step 8 — Run the Docker Container

Run the following command:

```bash
docker run -p 8000:8000 <DOCKER_USERNAME>/insurance-premium-api
```

The application will now run inside the Docker container.

The FastAPI application should be accessible at:

```text
http://localhost:8000
```

---

## 📖 FastAPI Swagger Documentation

FastAPI automatically provides interactive API documentation.

Open:

```text
http://localhost:8000/docs
```

You can use the Swagger UI to:

- View API endpoints
- View request parameters
- Send prediction requests
- Test API responses
- Verify that the application is working

---

# ☁️ AWS EC2 Deployment

The Dockerized FastAPI application can be deployed to an AWS EC2 instance.

---

## Step 1 — Create an EC2 Instance

Create an EC2 instance using the AWS Management Console.

An Ubuntu-based EC2 instance can be used for this project.

Make sure you have access to the instance through SSH or AWS EC2 Instance Connect.

---

## Step 2 — Connect to the EC2 Instance

Connect to the EC2 instance.

For example:

```bash
ssh -i your-key.pem ubuntu@<EC2_PUBLIC_IP>
```

Replace:

```text
<EC2_PUBLIC_IP>
```

with the public IP address of your EC2 instance.

---

# 🐳 Install Docker on EC2

## Step 3 — Install and Configure Docker

Run the following commands on the EC2 instance.

### a. Update the package list

```bash
sudo apt-get update
```

### b. Install Docker

```bash
sudo apt-get install -y docker.io
```

### c. Start Docker

```bash
sudo systemctl start docker
```

### d. Enable Docker

```bash
sudo systemctl enable docker
```

### e. Add the current user to the Docker group

```bash
sudo usermod -aG docker $USER
```

### f. Exit the EC2 instance

```bash
exit
```

---

# 🔄 Reconnect to the EC2 Instance

## Step 4 — Restart the EC2 Connection

Connect to the EC2 instance again.

This is required for the Docker group permissions to take effect.

Verify Docker installation:

```bash
docker --version
```

You should now be able to run Docker commands without using `sudo`.

---

# 📥 Pull the Docker Image on EC2

## Step 5 — Pull the Image

Run:

```bash
docker pull <DOCKER_USERNAME>/insurance-premium-api:latest
```

This downloads the Docker image from Docker Hub to your EC2 instance.

You can verify the downloaded image using:

```bash
docker images
```

---

# ▶️ Run the Docker Image on EC2

Run:

```bash
docker run -p 8000:8000 <DOCKER_USERNAME>/insurance-premium-api
```

The FastAPI application will now be running inside the Docker container on the EC2 instance.

You can verify that the container is running using:

```bash
docker ps
```

---

# 🔓 Configure AWS Security Group

## Step 6 — Change Security Group Settings

To access the FastAPI application from outside the EC2 instance, port `8000` must be allowed in the EC2 Security Group.

Go to:

```text
AWS Console
    ↓
EC2
    ↓
Instances
    ↓
Select Your Instance
    ↓
Security
    ↓
Security Groups
    ↓
Inbound Rules
    ↓
Edit Inbound Rules
```

Add a new inbound rule:

| Type | Protocol | Port | Source |
|------|----------|------|--------|
| Custom TCP | TCP | 8000 | Your IP / 0.0.0.0/0 |

For development/testing, you can use:

```text
0.0.0.0/0
```

> For production deployments, it is recommended to restrict access to trusted IP addresses instead of allowing traffic from `0.0.0.0/0`.

---

# 🧪 Check the API

## Step 7 — Access the API

Once the Docker container is running and port `8000` has been allowed through the EC2 Security Group, access the API using:

```text
http://<EC2_PUBLIC_IP>:8000
```

Replace:

```text
<EC2_PUBLIC_IP>
```

with the public IP address of your EC2 instance.

---

## 📖 Access FastAPI Swagger Documentation

Open:

```text
http://<EC2_PUBLIC_IP>:8000/docs
```

The Swagger UI allows you to interact with and test the API directly from your browser.

---

# 🔄 Complete Docker + AWS Deployment Workflow

```text
                    LOCAL MACHINE
                         │
                         ▼
                    Dockerfile
                         │
                         ▼
                  Docker Build
                         │
                         ▼
                   Docker Image
                         │
                         ▼
                    Docker Login
                         │
                         ▼
                  Docker Push
                         │
                         ▼
                     DOCKER HUB
                         │
                         │
                         ▼
                    AWS EC2
                         │
                         ▼
                  Docker Pull
                         │
                         ▼
                  Docker Run
                         │
                         ▼
                 Docker Container
                         │
                         ▼
                  FastAPI Server
                         │
                         ▼
              Port 8000 / API
                         │
                         ▼
          http://<EC2_PUBLIC_IP>:8000
```

---

# 🧠 Machine Learning Model

The Insurance Premium Predictor uses a **Random Forest** machine learning model for prediction.

### Machine Learning Workflow

```text
Raw Input Data
      │
      ▼
Data Cleaning
      │
      ▼
Data Preprocessing
      │
      ▼
Feature Engineering
      │
      ▼
Train-Test Split
      │
      ▼
Random Forest Model
      │
      ▼
Model Training
      │
      ▼
Model Evaluation
      │
      ▼
Saved Model
      │
      ▼
FastAPI Integration
      │
      ▼
Premium Prediction
```

The trained model is integrated with the FastAPI backend, allowing users to send input data through an API and receive the predicted insurance premium.

---

# 🔌 API

The FastAPI backend exposes the Machine Learning model through REST API endpoints.

## Local API

```text
http://localhost:8000
```

## Local Swagger Documentation

```text
http://localhost:8000/docs
```

## EC2 API

```text
http://<EC2_PUBLIC_IP>:8000
```

## EC2 Swagger Documentation

```text
http://<EC2_PUBLIC_IP>:8000/docs
```

The Swagger interface can be used to:

- View available endpoints
- View request parameters
- Submit prediction requests
- Test API responses
- Verify the deployed Machine Learning model

---

# 📌 Useful Docker Commands

## View Docker Images

```bash
docker images
```

## View Running Containers

```bash
docker ps
```

## View All Containers

```bash
docker ps -a
```

## Stop a Container

```bash
docker stop <CONTAINER_ID>
```

## Remove a Container

```bash
docker rm <CONTAINER_ID>
```

## Remove a Docker Image

```bash
docker rmi <IMAGE_ID>
```

## Pull the Latest Image

```bash
docker pull <DOCKER_USERNAME>/insurance-premium-api:latest
```

## Run the Latest Image

```bash
docker run -p 8000:8000 <DOCKER_USERNAME>/insurance-premium-api:latest
```

## Run Container in Detached Mode

If you want the application to continue running after closing the terminal:

```bash
docker run -d -p 8000:8000 <DOCKER_USERNAME>/insurance-premium-api:latest
```

## View Container Logs

```bash
docker logs <CONTAINER_ID>
```

---

# 🔧 Updating the Docker Image

Whenever you make changes to the application, rebuild the Docker image:

```bash
docker build -t <DOCKER_USERNAME>/insurance-premium-api .
```

Then push the updated image to Docker Hub:

```bash
docker push <DOCKER_USERNAME>/insurance-premium-api:latest
```

On the EC2 instance, pull the latest version:

```bash
docker pull <DOCKER_USERNAME>/insurance-premium-api:latest
```

Stop the old container:

```bash
docker stop <CONTAINER_ID>
```

Remove the old container:

```bash
docker rm <CONTAINER_ID>
```

Run the updated container:

```bash
docker run -d -p 8000:8000 <DOCKER_USERNAME>/insurance-premium-api:latest
```

---

# 🛡️ Production Considerations

For production deployment, consider the following:

- Restrict EC2 Security Group access
- Use HTTPS instead of HTTP
- Run the application behind Nginx
- Use an AWS Application Load Balancer
- Add authentication and authorization
- Use environment variables for sensitive configuration
- Add API logging and monitoring
- Use proper Docker image versioning
- Avoid relying only on the `latest` tag
- Configure automatic container restart policies
- Implement proper error handling and API validation



## 📄 License

This project is intended for educational and portfolio purposes.
