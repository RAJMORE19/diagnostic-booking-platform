# 📋 COMPLETE README.md FOR BLOOD TEST PLATFORM

Below is a comprehensive, step-by-step README that any visitor can follow to implement the entire project. It's written in a friendly, educational style with clear instructions.

---

```markdown
# 🩸 Blood Test Booking & Diagnostic E-Commerce Platform

> A production-grade healthcare platform built with **FastAPI**, **React**, **Docker**, **Kubernetes (EKS)**, **Terraform**, **Jenkins**, and **Argo CD** — designed to demonstrate real-world DevOps, AWS, CI/CD, DevSecOps, and SRE practices.

---

## 📌 Project Overview

This platform allows users to:
- 🔍 Browse blood test catalog
- 🛒 Add tests to cart
- 📅 Book home collection or diagnostic center visits
- 💳 Make payments (simulated)
- 📋 View booking history
- 🔐 Manage user profiles

**Architecture**: Microservices-based with 6 core services:
1. Auth Service
2. Test Catalog Service
3. Cart Service
4. Booking Service
5. Payment Service
6. Notification Service

---

## 🎯 Why This Project?

This project is specifically designed for **DevOps Engineers with 2-4 years of experience** aiming to transition into **AWS/Cloud DevOps roles**.

You will gain hands-on experience with:
- ✅ AWS (VPC, EKS, RDS, ECR, ALB, Route 53, IAM, S3, Secrets Manager)
- ✅ Infrastructure as Code (Terraform)
- ✅ Containerization (Docker)
- ✅ Kubernetes (EKS, Helm)
- ✅ CI/CD (Jenkins, Argo CD, GitOps)
- ✅ DevSecOps (SonarQube, Trivy, Dependency Scanning)
- ✅ Observability (Prometheus, Grafana, Loki)
- ✅ Production Incident Management
- ✅ Disaster Recovery & Cost Optimization

---

## 📚 Table of Contents

- [Technology Stack](#technology-stack)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Project Structure](#project-structure)
- [7-Day Implementation Roadmap](#7-day-implementation-roadmap)
- [Installation & Setup](#installation--setup)
- [Local Development](#local-development)
- [AWS Infrastructure](#aws-infrastructure)
- [Kubernetes Deployment](#kubernetes-deployment)
- [CI/CD Pipeline](#cicd-pipeline)
- [Monitoring & Observability](#monitoring--observability)
- [Troubleshooting Guide](#troubleshooting-guide)
- [Interview Preparation](#interview-preparation)
- [Contributing](#contributing)
- [License](#license)

---

## 🛠 Technology Stack

### Application Layer
| Component | Technology |
|-----------|------------|
| Frontend | React |
| Backend | Python + FastAPI |
| API | REST |
| Database | PostgreSQL |
| Cache | Redis |
| Object Storage | AWS S3 |

### Containerization & Orchestration
| Component | Technology |
|-----------|------------|
| Containerization | Docker |
| Local Environment | Docker Compose |
| Orchestration | Kubernetes |
| Managed Kubernetes | AWS EKS |
| Package Management | Helm |

### Infrastructure as Code
| Component | Technology |
|-----------|------------|
| IaC | Terraform |
| VPC | AWS VPC |
| Networking | Public/Private Subnets, NAT Gateway |

### CI/CD & GitOps
| Component | Technology |
|-----------|------------|
| Source Control | Git + GitHub |
| CI | Jenkins |
| GitOps | Argo CD |
| Container Registry | AWS ECR |

### Security & Quality
| Component | Technology |
|-----------|------------|
| Code Quality | SonarQube |
| Dependency Security | OWASP Dependency-Check |
| Image Security | Trivy |
| Secrets Management | AWS Secrets Manager |

### Observability
| Component | Technology |
|-----------|------------|
| Metrics | Prometheus |
| Dashboards | Grafana |
| Logs | Loki |
| AWS Monitoring | CloudWatch |

---

## 🏗 Architecture

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         END USER                                │
└─────────────────────────────┬───────────────────────────────────┘
                              │ HTTPS/TLS
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                      Route 53 DNS                               │
└─────────────────────────────┬───────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                        AWS ALB                                  │
└─────────────────────────────┬───────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                    AWS EKS (Kubernetes)                         │
│                                                                 │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐        │
│  │   Frontend   │  │ Auth Service │  │ Catalog Svc  │        │
│  │    React     │  │              │  │              │        │
│  └──────────────┘  └──────────────┘  └──────────────┘        │
│                                                                 │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐        │
│  │  Cart Svc    │  │ Booking Svc  │  │ Payment Svc  │        │
│  │              │  │              │  │              │        │
│  └──────────────┘  └──────────────┘  └──────────────┘        │
│                                                                 │
│  ┌──────────────┐                                              │
│  │ Notification │                                              │
│  │    Svc       │                                              │
│  └──────────────┘                                              │
└─────────────────────────────┬───────────────────────────────────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
        ▼                     ▼                     ▼
┌───────────────┐    ┌───────────────┐    ┌───────────────┐
│  PostgreSQL   │    │    Redis      │    │      S3       │
│     RDS       │    │    Cache      │    │   Documents   │
└───────────────┘    └───────────────┘    └───────────────┘
```

### DevOps Pipeline

```
┌─────────────┐
│  Developer  │
└──────┬──────┘
       │ git push
       ▼
┌─────────────┐
│   GitHub    │
└──────┬──────┘
       │ Pull Request
       ▼
┌─────────────┐
│   Jenkins   │
│             │
│ Unit Tests  │
│ Lint        │
│ SonarQube   │
│ Dependency  │
│ Docker Build│
│ Trivy Scan  │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  AWS ECR    │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  GitOps Repo│
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  Argo CD    │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  AWS EKS    │
└─────────────┘
```

---

## 📋 Prerequisites

Before starting, ensure you have:

### Local Development
- 🐍 Python 3.12+
- 📦 Node.js 18+
- 🐳 Docker 24+
- 🧰 Docker Compose 2.20+
- 🔧 Git 2.40+
- 📦 Terraform 1.6+
- ☸️ kubectl
- 🧰 Helm 3+
- 📦 AWS CLI 2.13+

### AWS Account
- Valid AWS account with administrative access (or sufficient permissions)
- AWS CLI configured with appropriate credentials
- Domain name (optional, for production)

### Tools to Install
```bash
# Install AWS CLI
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

# Install Terraform
wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform

# Install kubectl
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/

# Install Helm
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

---

## 📁 Project Structure

```
blood-test-platform/
│
├── README.md                           # This file
├── .gitignore                          # Git ignore rules
│
├── services/                           # Microservices
│   ├── auth-service/                   # Authentication & Users
│   │   ├── app.py
│   │   ├── requirements.txt
│   │   ├── Dockerfile
│   │   └── .dockerignore
│   ├── test-catalog-service/           # Test Catalog
│   │   ├── app.py
│   │   ├── requirements.txt
│   │   ├── Dockerfile
│   │   └── .dockerignore
│   ├── cart-service/                   # Shopping Cart
│   │   ├── app.py
│   │   ├── requirements.txt
│   │   ├── Dockerfile
│   │   └── .dockerignore
│   ├── booking-service/                # Booking Management
│   │   ├── app.py
│   │   ├── requirements.txt
│   │   ├── Dockerfile
│   │   └── .dockerignore
│   ├── payment-service/                # Payment Processing
│   │   ├── app.py
│   │   ├── requirements.txt
│   │   ├── Dockerfile
│   │   └── .dockerignore
│   └── notification-service/           # Notifications
│       ├── app.py
│       ├── requirements.txt
│       ├── Dockerfile
│       └── .dockerignore
│
├── frontend/                           # React Frontend
│   ├── public/
│   ├── src/
│   ├── package.json
│   ├── Dockerfile
│   └── .dockerignore
│
├── docker/                             # Docker Configuration
│   └── docker-compose.yml              # Local Development Compose
│
├── terraform/                          # Infrastructure as Code
│   ├── modules/
│   │   ├── vpc/                        # VPC Module
│   │   ├── iam/                        # IAM Module
│   │   ├── ecr/                        # ECR Module
│   │   ├── rds/                        # RDS Module
│   │   ├── eks/                        # EKS Module (Day 4+)
│   │   └── monitoring/                 # Monitoring Module
│   └── environments/
│       ├── dev/                        # Development Environment
│       ├── staging/                    # Staging Environment
│       └── prod/                       # Production Environment
│
├── helm/                               # Helm Charts
│   └── blood-test-platform/
│       ├── Chart.yaml
│       ├── values.yaml
│       ├── values-dev.yaml
│       ├── values-staging.yaml
│       ├── values-prod.yaml
│       └── templates/
│           ├── deployment.yaml
│           ├── service.yaml
│           ├── ingress.yaml
│           ├── configmap.yaml
│           └── hpa.yaml
│
├── jenkins/                            # CI Configuration
│   └── Jenkinsfile
│
├── gitops/                             # GitOps Configuration
│   └── applications/
│       ├── dev/
│       ├── staging/
│       └── prod/
│
├── monitoring/                         # Observability
│   ├── prometheus/
│   ├── grafana/
│   └── loki/
│
├── scripts/                            # Utility Scripts
│   ├── setup-local.sh
│   ├── deploy-dev.sh
│   └── cleanup.sh
│
├── tests/                              # Test Files
│   └── ...
│
└── docs/                               # Documentation
    ├── architecture.md
    ├── aws-architecture.md
    ├── networking.md
    ├── kubernetes.md
    ├── terraform.md
    ├── cicd.md
    ├── gitops.md
    ├── security.md
    ├── monitoring.md
    ├── logging.md
    ├── troubleshooting.md
    ├── disaster-recovery.md
    ├── cost-optimization.md
    └── interview-questions.md
```

---

## 🗓 7-Day Implementation Roadmap

### Day 1: Application Foundation
**Goal**: Establish repository structure and basic FastAPI service

✅ **Must Have**:
- [ ] GitHub repository created
- [ ] Project structure initialized
- [ ] `.gitignore` configured
- [ ] `README.md` created
- [ ] Test Catalog Service with FastAPI
- [ ] Health endpoints (`/health`, `/ready`)
- [ ] Basic `/tests` endpoint
- [ ] Dockerfile for Catalog Service
- [ ] Docker image built and tested locally
- [ ] Git commit and push

📝 **Commands**:
```bash
# Initialize repository
mkdir -p ~/blood-test-platform
cd ~/blood-test-platform
git init
git branch -M main

# Create directories
mkdir -p services/test-catalog-service
mkdir -p frontend docker docs scripts tests jenkins gitops helm terraform monitoring

# Create initial files
touch README.md .gitignore
touch docs/architecture.md docs/development.md

# Create Catalog Service
cd services/test-catalog-service
python3 -m venv .venv
source .venv/bin/activate
pip install fastapi uvicorn[standard] pytest httpx
```

### Day 2: Microservices + Database
**Goal**: Build all 6 services with PostgreSQL & Redis

✅ **Must Have**:
- [ ] All 6 services implemented
- [ ] PostgreSQL database connection
- [ ] Redis cache integration
- [ ] Booking flow working
- [ ] API endpoints complete
- [ ] Health checks for all services
- [ ] Docker Compose local environment
- [ ] End-to-end testing passing

### Day 3: AWS Foundation
**Goal**: AWS infrastructure with VPC, ECR, RDS

✅ **Must Have**:
- [ ] AWS CLI configured
- [ ] Terraform installed
- [ ] VPC with public/private subnets
- [ ] Internet Gateway
- [ ] Route tables configured
- [ ] Security Groups
- [ ] ECR repositories created
- [ ] RDS PostgreSQL deployed
- [ ] Terraform state management

### Day 4: EKS + Kubernetes
**Goal**: Deploy application on AWS EKS

✅ **Must Have**:
- [ ] EKS cluster provisioned
- [ ] Kubernetes Deployments
- [ ] Kubernetes Services
- [ ] Ingress configured
- [ ] ConfigMaps & Secrets
- [ ] Probes (readiness/liveness)
- [ ] Resource requests/limits
- [ ] HPA configured
- [ ] PDB configured

### Day 5: CI/CD Pipeline
**Goal**: Automate build, test, and deployment

✅ **Must Have**:
- [ ] Jenkins pipeline
- [ ] Unit tests running
- [ ] SonarQube integration
- [ ] Dependency scanning
- [ ] Docker build automation
- [ ] Trivy security scanning
- [ ] ECR push
- [ ] GitOps repository setup

### Day 6: GitOps + Observability
**Goal**: Implement GitOps and monitoring

✅ **Must Have**:
- [ ] Argo CD installed
- [ ] GitOps repository structure
- [ ] Helm charts
- [ ] Argo CD sync working
- [ ] Prometheus metrics
- [ ] Grafana dashboards
- [ ] Loki logs
- [ ] Basic alerts configured

### Day 7: Hardening + Troubleshooting + Documentation
**Goal**: Production-readiness and interview prep

✅ **Must Have**:
- [ ] Production hardening
- [ ] Incident simulations
- [ ] Troubleshooting runbooks
- [ ] High availability patterns
- [ ] Backup/restore procedures
- [ ] Cost optimization analysis
- [ ] Complete documentation
- [ ] Architecture diagrams
- [ ] Interview Q&A prep

---

## 🚀 Installation & Setup

### Step 1: Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/blood-test-platform.git
cd blood-test-platform
```

### Step 2: Local Development Setup

```bash
# Create Python virtual environment
python3 -m venv .venv
source .venv/bin/activate

# Install dependencies for each service
cd services/auth-service
pip install -r requirements.txt
cd ../test-catalog-service
pip install -r requirements.txt
# ... repeat for all services

# Install frontend dependencies
cd ../../frontend
npm install
```

### Step 3: Run with Docker Compose

```bash
# Start all services locally
docker-compose -f docker/docker-compose.yml up -d

# Verify services are running
docker ps

# Check health endpoints
curl http://localhost:8000/health     # Catalog Service
curl http://localhost:8001/health     # Auth Service
curl http://localhost:8002/health     # Cart Service
# ... etc
```

### Step 4: Verify Local Application

| Service | Port | Health Endpoint |
|---------|------|-----------------|
| Auth Service | 8001 | `http://localhost:8001/health` |
| Catalog Service | 8000 | `http://localhost:8000/health` |
| Cart Service | 8002 | `http://localhost:8002/health` |
| Booking Service | 8003 | `http://localhost:8003/health` |
| Payment Service | 8004 | `http://localhost:8004/health` |
| Notification Service | 8005 | `http://localhost:8005/health` |
| Frontend | 3000 | `http://localhost:3000` |
| PostgreSQL | 5432 | - |
| Redis | 6379 | - |

---

## ☁️ AWS Infrastructure

### Prerequisites

```bash
# Configure AWS CLI
aws configure
# Enter: Access Key, Secret Key, Region (ap-south-1), Output (json)

# Verify AWS access
aws sts get-caller-identity
```

### Terraform Setup

```bash
cd terraform/environments/dev

# Initialize Terraform
terraform init

# Format and validate
terraform fmt -recursive
terraform validate

# Review changes
terraform plan

# Apply infrastructure
terraform apply
# Type 'yes' when prompted

# Verify resources
terraform output
```

### AWS Resource Breakdown

| Resource | Configuration | Purpose |
|----------|---------------|---------|
| VPC | 10.0.0.0/16 | Network isolation |
| Public Subnets | 10.0.1.0/24, 10.0.2.0/24 | ALB, NAT Gateway |
| Private Subnets | 10.0.11.0/24, 10.0.12.0/24 | EKS, RDS |
| Internet Gateway | - | Internet access |
| NAT Gateway | - | Outbound internet for private subnets |
| ECR | 6 repositories | Container images |
| RDS | PostgreSQL | Application database |
| EKS | - | Kubernetes cluster |
| ALB | - | Traffic routing |
| Route 53 | - | DNS management |

### Cost Management

⚠️ **Important**: AWS resources cost money. Always clean up when not in use:

```bash
# Destroy all infrastructure (BE CAREFUL!)
cd terraform/environments/dev
terraform destroy
```

**Cost Estimation (ap-south-1)**:
- RDS (db.t4g.micro): ~₹2,000/month
- EKS (control plane): ~₹5,000/month
- NAT Gateway: ~₹2,500/month
- EC2 (t3.medium × 2): ~₹3,000/month
- ALB: ~₹1,000/month

**Total**: ~₹13,500/month ≈ $160/month

---

## ☸️ Kubernetes Deployment

### Prerequisites

```bash
# Update kubeconfig
aws eks update-kubeconfig --region ap-south-1 --name blood-test-cluster

# Verify cluster access
kubectl cluster-info
kubectl get nodes
```

### Helm Deployment

```bash
# Install the Helm chart
cd helm/blood-test-platform

# For development environment
helm upgrade --install blood-test-dev . \
  -f values-dev.yaml \
  --namespace blood-test-dev \
  --create-namespace

# For staging
helm upgrade --install blood-test-staging . \
  -f values-staging.yaml \
  --namespace blood-test-staging \
  --create-namespace

# For production
helm upgrade --install blood-test-prod . \
  -f values-prod.yaml \
  --namespace blood-test-prod \
  --create-namespace

# Verify deployment
kubectl get pods -n blood-test-dev
kubectl get services -n blood-test-dev
kubectl get ingress -n blood-test-dev
```

### Kubernetes Resources

| Resource | Purpose |
|----------|---------|
| Deployments | Application pods |
| Services | Internal networking |
| Ingress | External access |
| ConfigMaps | Non-sensitive config |
| Secrets | Sensitive data |
| HPA | Auto-scaling |
| PDB | Pod disruption budgets |
| ServiceAccount | Kubernetes identity |

### Service Endpoints

After deployment, access via:
```bash
# Get ALB DNS name
kubectl get ingress -n blood-test-dev

# Or via Route 53 (if configured)
https://api.yourdomain.com
```

---

## 🔄 CI/CD Pipeline

### Jenkins Pipeline

The `Jenkinsfile` defines:

```groovy
pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Unit Tests') {
            steps {
                sh 'python -m pytest tests/'
            }
        }
        
        stage('SonarQube') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        
        stage('Dependency Scan') {
            steps {
                sh 'dependency-check --scan .'
            }
        }
        
        stage('Docker Build') {
            steps {
                sh 'docker build -t ${IMAGE_TAG} .'
            }
        }
        
        stage('Trivy Scan') {
            steps {
                sh 'trivy image ${IMAGE_TAG}'
            }
        }
        
        stage('Push to ECR') {
            steps {
                sh 'aws ecr get-login-password | docker login --username AWS --password-stdin ${ECR_URL}'
                sh 'docker push ${IMAGE_TAG}'
            }
        }
        
        stage('Update GitOps') {
            steps {
                sh './scripts/update-gitops.sh ${IMAGE_TAG}'
            }
        }
    }
}
```

### GitOps with Argo CD

```bash
# Install Argo CD
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Port forward to access UI
kubectl port-forward svc/argocd-server -n argocd 8080:443

# Login (default password is the pod name)
argocd login localhost:8080

# Create application
argocd app create blood-test-dev \
  --repo https://github.com/YOUR_USERNAME/gitops-repo.git \
  --path overlays/dev \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace blood-test-dev \
  --sync-policy automated

# Sync application
argocd app sync blood-test-dev
```

---

## 📊 Monitoring & Observability

### Prometheus

```bash
# Install Prometheus
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install prometheus prometheus-community/prometheus \
  -f monitoring/prometheus/values.yaml \
  -n monitoring --create-namespace

# Port forward for access
kubectl port-forward svc/prometheus-server -n monitoring 9090:80
```

### Grafana

```bash
# Install Grafana
helm repo add grafana https://grafana.github.io/helm-charts
helm install grafana grafana/grafana \
  -f monitoring/grafana/values.yaml \
  -n monitoring

# Get admin password
kubectl get secret grafana -n monitoring -o jsonpath="{.data.admin-password}" | base64 --decode

# Port forward
kubectl port-forward svc/grafana -n monitoring 3000:80
```

### Loki

```bash
# Install Loki
helm repo add grafana https://grafana.github.io/helm-charts
helm install loki grafana/loki-stack \
  -f monitoring/loki/values.yaml \
  -n monitoring
```

### Pre-built Dashboards

| Dashboard | URL |
|-----------|-----|
| Kubernetes Cluster | `http://grafana:3000/d/kubernetes-cluster` |
| Application Performance | `http://grafana:3000/d/application-metrics` |
| API Endpoint Monitoring | `http://grafana:3000/d/api-monitoring` |

---

## 🔧 Troubleshooting Guide

### Common Issues & Solutions

#### 1. Container Won't Start (CrashLoopBackOff)

```bash
# Check logs
kubectl logs <pod-name> -n <namespace>

# Check events
kubectl describe pod <pod-name> -n <namespace>

# Common fixes:
# - Check environment variables
# - Verify database connectivity
# - Check resource limits
```

#### 2. Image Pull Error (ImagePullBackOff)

```bash
# Verify image exists in ECR
aws ecr describe-images --repository-name <repo-name>

# Check ECR permissions
aws sts get-caller-identity

# Fix: Ensure EC2/EKS node has ECR permissions
```

#### 3. Database Connection Issues

```bash
# Test RDS connectivity
nc -zv <rds-endpoint> 5432

# Check security groups
aws ec2 describe-security-groups --group-ids <sg-id>

# Common fixes:
# - Add EKS node SG to RDS inbound rules
# - Verify database credentials in Secrets Manager
# - Check VPC routing
```

#### 4. Ingress Not Working

```bash
# Check ingress controller
kubectl get pods -n ingress-nginx

# Check ingress rules
kubectl describe ingress -n <namespace>

# Verify ALB
aws elbv2 describe-load-balancers

# Common fixes:
# - Update ingress rules
# - Check TLS certificate in ACM
# - Verify Route 53 record
```

#### 5. Jenkins Pipeline Fails

```bash
# Check Jenkins logs
sudo journalctl -u jenkins -f

# Verify Jenkins plugins are installed
# Check Jenkinsfile syntax
# Review Jenkins agent configuration
```

#### 6. Terraform Apply Fails

```bash
# Detailed error
terraform plan -detailed-exitcode

# Check state
terraform state list

# Fix:
# - Check AWS credentials
# - Verify IAM permissions
# - Check for conflicting resources
```

### Quick Diagnostic Commands

```bash
# Kubernetes Diagnostics
kubectl get nodes
kubectl get pods -A
kubectl top pods -A

# AWS Diagnostics
aws ec2 describe-instances --query 'Reservations[*].Instances[*].State'
aws rds describe-db-instances --query 'DBInstances[*].DBInstanceStatus'
aws eks describe-cluster --name blood-test-cluster

# Network Diagnostics
kubectl run test-pod --rm -it --image=busybox -- /bin/sh
# Inside pod: nslookup <service-name>
```

---

## 💼 Interview Preparation

### Key Topics to Master

#### AWS
- VPC, Subnets, Route Tables, NAT Gateway
- IAM: Users, Roles, Policies, Least Privilege
- ECR: Image Management, Security Scanning
- RDS: Multi-AZ, Backups, Performance
- EKS: Control Plane, Node Groups, Networking
- ALB: Listeners, Target Groups, Health Checks
- Route 53: DNS, Records, Alias
- Secrets Manager: Secure Credential Storage

#### Kubernetes
- Pods, Deployments, Services, Ingress
- ConfigMaps, Secrets
- Probes (liveness, readiness, startup)
- Resource Management (requests, limits)
- HPA (Horizontal Pod Autoscaler)
- PDB (Pod Disruption Budgets)
- RBAC (Role-Based Access Control)

#### Terraform
- Providers, Resources, Data Sources
- State Management (remote, locking)
- Modules (creation, composition)
- Variables, Outputs, Locals
- Workspaces vs Environment Directories
- Drift Detection and Handling

#### CI/CD
- Jenkins Pipeline (Declarative)
- Jenkins Shared Libraries
- Integration with GitHub, ECR, Kubernetes
- Security Scanning (SonarQube, Trivy, Dependency Check)
- Argo CD: GitOps, Sync Policies, Auto-Sync

#### Observability
- Prometheus Metrics, AlertManager
- Grafana Dashboards
- Loki Log Aggregation
- CloudWatch for AWS Resources

### Sample Interview Questions

#### Q: Why did you create separate liveness and readiness probes?
> Liveness probes check if the application is alive and restart the pod if it's unresponsive. Readiness probes check if the application is ready to receive traffic. For example, if PostgreSQL is unavailable, the pod should remain alive (don't restart) but shouldn't receive traffic (unready).

#### Q: Why do you use IAM Roles instead of Access Keys on EC2?
> IAM Roles provide temporary credentials that are automatically rotated. Access Keys are long-lived and can be compromised. With IAM Roles, I follow the principle of least privilege and don't have to manage credentials in code.

#### Q: Why did you choose Terraform over CloudFormation?
> Terraform is cloud-agnostic, supports multiple providers, has a larger module ecosystem, and provides better plan/apply workflow. It's also more widely used in multi-cloud environments.

#### Q: Why GitOps over traditional CI/CD?
> GitOps provides a single source of truth for the desired state. Argo CD continuously reconciles the actual state with the desired state from Git. This gives us automatic drift correction, auditability, and easier rollbacks.

---

## 📝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'feat: add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Commit Convention

Use conventional commits:
- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation
- `style:` Code style
- `refactor:` Code refactoring
- `perf:` Performance improvement
- `test:` Testing
- `chore:` Maintenance

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- FastAPI for the excellent Python framework
- React team for the frontend framework
- HashiCorp for Terraform
- CNCF for Kubernetes, Prometheus, and Argo CD
- AWS for cloud infrastructure

---

## 📞 Contact

- **Author**: Raj More
- **GitHub**: [@yourusername](https://github.com/yourusername)
- **Email**: your.email@example.com

---

## 🔗 Useful Links

- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [React Documentation](https://reactjs.org/docs/)
- [Docker Documentation](https://docs.docker.com/)
- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Terraform Documentation](https://developer.hashicorp.com/terraform/docs)
- [AWS Documentation](https://docs.aws.amazon.com/)
- [Argo CD Documentation](https://argo-cd.readthedocs.io/)

---

**⭐ Star this repository if you find it helpful!**
```

---

## 📋 Quick Reference Commands

Here's a handy cheat sheet for the most common commands:

### Local Development
```bash
# Start everything
docker-compose -f docker/docker-compose.yml up -d

# Stop everything
docker-compose -f docker/docker-compose.yml down

# View logs
docker-compose -f docker/docker-compose.yml logs -f

# Rebuild and restart a specific service
docker-compose -f docker/docker-compose.yml up -d --build catalog-service
```

### AWS CLI
```bash
# Check identity
aws sts get-caller-identity

# List resources
aws ec2 describe-vpcs
aws ecr describe-repositories
aws rds describe-db-instances
aws eks list-clusters
```

### Terraform
```bash
terraform init
terraform fmt -recursive
terraform validate
terraform plan
terraform apply
terraform destroy
terraform state list
terraform output
```

### Kubernetes
```bash
kubectl get nodes
kubectl get pods -A
kubectl describe pod <pod>
kubectl logs <pod>
kubectl exec -it <pod> -- /bin/bash
kubectl port-forward <pod> 8080:80
kubectl apply -f <file>
kubectl delete -f <file>
kubectl rollout restart deployment <deployment>
```

### Helm
```bash
helm list -A
helm install <release> <chart>
helm upgrade <release> <chart>
helm uninstall <release>
helm template <release> <chart>
```

---

This README provides a **complete, step-by-step guide** that any visitor can follow to implement the entire Blood Test Booking Platform. It's structured to be:
1. **Educational** - explains WHY as well as HOW
2. **Practical** - includes actual commands to run
3. **Complete** - covers every day of the 7-day roadmap
4. **Professional** - interview preparation included
