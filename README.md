# DevOps TP3 - Kubernetes Deployment Comparison

A practical comparison of traditional Kubernetes manifests vs Helm Charts for application deployment, featuring two independent Jenkins CI/CD pipelines.

## 🎯 Project Overview

This project demonstrates two approaches to deploying a containerized application (`bahabouali/my-app:latest`) on Kubernetes:

1. **Traditional approach**: Direct kubectl commands with static YAML manifests
2. **Modern approach**: Helm Charts with templating and release management

Both methods deploy the same application: 2 replicas exposed on port 8080 via a LoadBalancer service.

## 📁 Project Structure

```
├── Jenkinsfile              # Traditional kubectl pipeline
├── Jenkinsfile-helm         # Helm-based pipeline
├── k8s/                    # Static Kubernetes manifests
│   ├── deployment.yaml
│   └── service.yaml
└── helm-charts/            # Helm chart with templates
    ├── Chart.yaml
    ├── values.yaml
    └── templates/
```

## 🚀 Quick Start

### Traditional Deployment (kubectl)
```bash
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
```

### Helm Deployment
```bash
helm install my-app-release ./helm-charts
```

## 🔄 CI/CD Pipelines

Both Jenkinsfiles are configured for "Pipeline script from SCM" and include:
- Validation stages
- Automated deployment to Kubernetes
- Health checks and verification
- Error handling with detailed logs

## 📊 Key Differences

| Feature | Traditional | Helm |
|---------|-------------|------|
| **Rollback** | Manual | `helm rollback` |
| **Configuration** | Hard-coded | Dynamic values |
| **Versioning** | None | Full history |
| **Environments** | Duplicate files | Override values |

## 🛠️ Prerequisites

- Kubernetes cluster (Minikube/Docker Desktop/Cloud)
- kubectl configured
- Helm 3+ (for Helm deployment)
- Jenkins with Kubernetes plugin

## 📝 Documentation

See [RAPPORT.md](RAPPORT.md) for detailed analysis in French, including architecture diagrams, pipeline explanations, and best practices.

## 👤 Author

**Baha Bouali** - DevOps Practice Project
