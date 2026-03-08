# 🚀 Jenkins CI/CD Pipeline with Docker & DockerHub

## 📌 Project Overview
This project demonstrates a complete CI/CD pipeline using Jenkins that automates the application build and deployment process.

The pipeline performs the following steps:

- Pulls source code from GitHub
- Builds a Docker image
- Pushes the image to DockerHub
- Deploys the container automatically

This project simulates a real-world DevOps workflow used in production environments.

---

# 🏗 Architecture

```
Developer
   │
   │ Push Code
   ▼
GitHub Repository
   │
   ▼
Jenkins CI/CD Pipeline
   │
   │ Build Docker Image
   ▼
Docker Engine
   │
   │ Push Image
   ▼
DockerHub Registry
   │
   ▼
Docker Container Deployment
   │
   ▼
Application Available at http://SERVER-IP:8081
```

---

# 🛠 Tech Stack

- Jenkins
- Docker
- DockerHub
- Git & GitHub
- Linux (Ubuntu)
- CI/CD Pipeline

---

# ⚙️ Project Structure

```
Jenkins-CiCD-Project
│
├── Dockerfile
├── Jenkinsfile
├── index.html
└── README.md
```

---

# 🔧 Jenkins Pipeline Stages

The pipeline contains the following stages:

### 1️⃣ Clone Repository
Pulls source code from GitHub.

### 2️⃣ Build Docker Image
Builds a Docker image using the Dockerfile.

### 3️⃣ Push Docker Image
Pushes the Docker image to DockerHub securely using Jenkins credentials.

### 4️⃣ Deploy Container
Runs the Docker container from the pushed image.

---

# 📄 Jenkinsfile

```groovy
pipeline {
    agent any

    environment {
        IMAGE_NAME = "gayaskhan1/jenkins-docker-ci-cd"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/gayaskhan1/devops-projects.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {

                    sh '''
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    docker push $IMAGE_NAME
                    '''
                }
            }
        }

        stage('Deploy Container') {
            steps {
                sh 'docker run -d -p 8081:3000 $IMAGE_NAME'
            }
        }

    }
}
```

---

# 🔐 Secure Credentials Management

DockerHub credentials are securely stored in Jenkins Credentials Manager and accessed in the pipeline using:

```
credentialsId: dockerhub-creds
```

This ensures that sensitive information is not exposed in the Jenkinsfile.

---

# ▶️ How to Run This Project

### Step 1
Install Jenkins and Docker on Ubuntu.

### Step 2
Create a Jenkins Pipeline job.

### Step 3
Connect the GitHub repository.

### Step 4
Add DockerHub credentials in Jenkins.

### Step 5
Run **Build Now** in Jenkins.

---

# 🔍 Verification

Check Docker images:

```
docker images
```

Check running containers:

```
docker ps
```

Open application:

```
http://SERVER-IP:8081
```

---

# 🎯 CI/CD Workflow

```
Developer pushes code → GitHub
        ↓
Jenkins triggers pipeline
        ↓
Docker image built
        ↓
Image pushed to DockerHub
        ↓
Container deployed automatically
```

---

# 📌 Future Improvements

- Add GitHub Webhooks
- Deploy application on Kubernetes
- Integrate SonarQube for code quality
- Add Terraform infrastructure automation

---

# 👨‍💻 Author

Mohd Gayasuddin Khan  
DevOps Engineer

GitHub  
https://github.com/gayaskhan1

LinkedIn  
https://www.linkedin.com/in/mohd-gayasuddin-khan-59771a152/
