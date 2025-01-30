# CI/CD Pipeline Repository

Welcome to the **Kavetec CI/CD** repository! This project is designed to demonstrate the implementation of a Continuous Integration and Continuous Deployment (CI/CD) pipeline using Jenkins, Docker, SonarQube, and Kubernetes.

## 📌 Repository Overview

This repository contains scripts, configuration files, and automation workflows for setting up a CI/CD pipeline that:
1. **Pulls code** from a GitHub repository
2. **Builds the application** using Maven
3. **Runs code analysis** with SonarQube
4. **Creates a Docker image** and pushes it to DockerHub
5. **Deploys the application** to a Kubernetes cluster (EKS)

## 🚀 Getting Started

### Prerequisites
Before setting up the pipeline, ensure you have the following installed:
- **Jenkins** with necessary plugins
- **Git** for version control
- **Apache Maven** for building the project
- **SonarQube** for code quality analysis
- **Docker** for containerization
- **Kubernetes** (EKS) for deployment

### 1️⃣ Clone the Repository
```sh
git clone https://github.com/DivineTheAnalyst/CICD-Pipeline.git
cd CICD
```

### 2️⃣ Configure Jenkins Pipeline
- Create a new **Jenkins Pipeline Job**
- Point it to this GitHub repository
- Use the `Jenkinsfile` provided in this repo

### 3️⃣ Run the Pipeline
Trigger the Jenkins job to:
- Fetch the latest code
- Run tests and analysis
- Build and push Docker images
- Deploy to Kubernetes

### 4️⃣ Verify Deployment
Once the pipeline completes successfully, verify that the application is running in Kubernetes:
```sh
kubectl get pods
kubectl get services
```

## 🏆 Learning Outcome
By working with this repository, you will understand how to:
- Implement a CI/CD pipeline
- Automate software testing and deployment
- Integrate tools like Jenkins, SonarQube, Docker, and Kubernetes

Happy Automating! 🚀

