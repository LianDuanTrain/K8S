## Topics         
- 

# Dashboard
- Web-based Kubernetes user interface
- Deploys with a minimal RBAC configuration by default 
- Supports logging in with a Bearer Token
Installing the Kubernetes Metrics Server 
The Kubernetes Metrics Server is an aggregator of resource usage data in K8S (Minikube)      
- `minikube addons enable metrics-server`
- `kubectl apply -f https://raw.githubusercontent.com/LianDuanTrain/K8S/main/3-Core-Concepts/springbootdemo-service-v1.yaml`  
# Using Dashboard
- Navigation
- Admin Overview
- Workloads
- Services
- Storage
- Config Maps and Secrets
- Logs viewer