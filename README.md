# Jenkins + SonarQube + Docker — CI/CD Pipeline

[![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=flat&logo=jenkins&logoColor=white)](https://www.jenkins.io/)
[![SonarQube](https://img.shields.io/badge/SonarQube-4E9BCD?style=flat&logo=sonarqube&logoColor=white)](https://www.sonarqube.org/)
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)](https://www.docker.com/)

A complete DevOps pipeline that integrates Jenkins for orchestration, SonarQube for static code analysis and quality gates, and Docker for containerized deployment.

## Pipeline Stages

```
SCM Checkout → SonarQube Analysis → Quality Gate → Docker Build → Deploy
```

| Stage | Tool | Description |
|---|---|---|
| Source Control | Jenkins SCM | Pulls latest code from the repository |
| Code Analysis | SonarQube + SonarScanner | Runs static analysis, detects bugs, vulnerabilities and code smells |
| Quality Gate | SonarQube | Blocks pipeline if code quality thresholds are not met |
| Containerization | Docker | Builds and packages the application image |

## Prerequisites

- Jenkins with the following plugins: SonarQube Scanner, Pipeline
- SonarQube server (can be run via Docker)
- Docker installed on the Jenkins agent
- SonarScanner configured in Jenkins Global Tool Configuration

## Setup

### 1. Start SonarQube

```bash
docker run -d --name sonarqube -p 9000:9000 sonarqube:lts-community
```

### 2. Configure Jenkins

- Add SonarQube server in **Manage Jenkins → Configure System → SonarQube servers**
- Add SonarScanner in **Manage Jenkins → Global Tool Configuration → SonarQube Scanner**

### 3. Create the Pipeline

Create a new Jenkins Pipeline job pointing to this repository. The `Jenkinsfile` at the root will be automatically detected.

### 4. Run

Trigger the pipeline manually or set up a webhook for automatic execution on push.

## Project Structure

```
.
├── Jenkinsfile          # Pipeline definition
├── Dockerfile           # Container image build
├── index.html           # Sample web application
└── vendor/              # Dependencies
```

## Key Concepts

- **Declarative pipeline as code** — the entire CI/CD flow lives in version control
- **Shift-left quality** — code analysis runs before any deployment
- **Quality gates** — the pipeline fails fast if standards are not met, preventing bad code from reaching production
