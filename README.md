# 🚀 End-to-End DevSecOps CI/CD Pipeline with Security & Monitoring

A production-style **DevSecOps CI/CD pipeline** that automates building, testing, security scanning, containerization, deployment, and monitoring of a Java Spring Boot web application.

> Built as part of PG-DITISS Course in Pune — demonstrating real-world DevSecOps practices used in enterprise environments.

---

## 📌 Project Overview

This project implements a fully automated CI/CD pipeline that integrates **security at every stage** — from code commit to production deployment — with real-time monitoring using Prometheus and Grafana.

The application under test is a **Board Game Listing Web App** (Java Spring Boot + AWS EC2), used as a realistic target to demonstrate the full pipeline.

---

## 🏗️ Architecture

```
Developer
    │
    ▼
GitHub (Code Push)
    │
    ▼
Jenkins (CI/CD Orchestration)
    │
    ├─── Maven Compile & Test
    │
    ├─── SonarQube (SAST - Static Code Analysis)
    │
    ├─── OWASP Dependency-Check (Vulnerable Dependencies)
    │
    ├─── Docker Build & Push (DockerHub)
    │
    ├─── Trivy (Container Image Vulnerability Scan)
    │
    └─── Kubernetes Deploy (Pods + Services)
              │
              ▼
        Prometheus + Blackbox Exporter
              │
              ▼
          Grafana Dashboard
```

---

## 🔧 Tech Stack

| Category | Tools |
|---|---|
| **CI/CD** | Jenkins, GitHub, Maven |
| **Language/Framework** | Java 17, Spring Boot |
| **SAST** | SonarQube |
| **Dependency Scanning** | OWASP Dependency-Check |
| **Container Security** | Trivy |
| **Containerization** | Docker |
| **Orchestration** | Kubernetes (Pods, Deployments, Services) |
| **Monitoring** | Prometheus, Blackbox Exporter, Grafana |
| **Cloud** | AWS EC2 |

---

## 🔄 Pipeline Stages

### Stage 1 — Compile
```groovy
stage('Compile') {
    steps {
        sh 'mvn compile'
    }
}
```

### Stage 2 — Test
```groovy
stage('Test') {
    steps {
        sh 'mvn test'
    }
}
```

### Stage 3 — Build
```groovy
stage('Build') {
    steps {
        sh 'mvn package'
    }
}
```

### Stage 4 — Security Scanning
- **SonarQube** — Static Application Security Testing (SAST), code quality analysis
- **OWASP Dependency-Check** — Scans Maven dependencies for known CVEs
- **Trivy** — Scans Docker images for OS and library vulnerabilities

### Stage 5 — Containerize & Push
- Application packaged into a Docker image using `Dockerfile`
- Image pushed to DockerHub registry

### Stage 6 — Deploy to Kubernetes
- Kubernetes `Deployment` and `Service` applied via `deployment-service.yaml`
- App exposed via NodePort/LoadBalancer service

### Stage 7 — Monitor
- **Prometheus** scrapes metrics from the application and infrastructure
- **Blackbox Exporter** monitors endpoint availability (uptime probing)
- **Grafana** visualizes all metrics in real-time dashboards

---

## 📁 Repository Structure

```
├── Jenkinsfile.txt          # Jenkins pipeline definition
├── Dockerfile.txt           # Docker image build instructions
├── deployment-service.yaml  # Kubernetes Deployment + Service manifest
├── pom.xml                  # Maven build configuration
├── sonar-project.properties # SonarQube project config
├── mvnw / mvnw.cmd          # Maven wrapper scripts
└── README.md
```

---

## 🛡️ Security Features

- **SAST** with SonarQube catches code-level vulnerabilities before build
- **OWASP Dependency-Check** identifies vulnerable third-party libraries
- **Trivy** ensures container images are scanned before deployment
- **Pipeline fails** if critical vulnerabilities are found — security as a gate, not an afterthought

---

## 📊 Monitoring Setup

| Tool | Purpose |
|---|---|
| Prometheus | Metrics collection from app + infra |
| Blackbox Exporter | HTTP endpoint uptime monitoring |
| Grafana | Visualization dashboards |

---

## 🚀 How to Run

### Prerequisites
- Jenkins server (with JDK 17 and Maven 3 configured as tools)
- SonarQube server running
- Docker installed and DockerHub credentials configured in Jenkins
- Kubernetes cluster (Minikube or cloud-based)
- Prometheus + Grafana stack deployed

### Steps

1. Clone this repository
```bash
git clone https://github.com/coderritesh/End-to-End-DevSecOps-CI-CD-Pipeline-with-Security-Monitoring.git
```

2. Configure Jenkins:
   - Add DockerHub credentials (`docker-cred`)
   - Add SonarQube server in Jenkins settings
   - Install required plugins: SonarQube Scanner, OWASP Dependency-Check, Docker Pipeline, Kubernetes

3. Create a Jenkins Pipeline job pointing to this repo's `Jenkinsfile`

4. Run the pipeline — all stages execute automatically

5. Access Grafana dashboard to monitor the deployed application

---



## 🎯 Key Learnings

- Integrating security tools (SonarQube, OWASP, Trivy) into CI/CD pipelines
- Container image vulnerability scanning before deployment
- Kubernetes deployment and service configuration
- Real-time application monitoring with Prometheus and Grafana
- End-to-end automation from code push to production

---

## 👤 Author

**Ritesh Gurav**
- 🔗 [LinkedIn](https://linkedin.com/in/ritesh-gurav)
- 💻 [GitHub](https://github.com/coderritesh)
- 📧 riteshgurav001@gmail.com
