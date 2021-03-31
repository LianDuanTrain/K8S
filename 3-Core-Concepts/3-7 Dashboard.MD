# Dashboard  
## What is Dashboard?
- Web-based Kubernetes user interface
- Deploys with a minimal RBAC configuration by default 
- Supports logging in with a Bearer Token
## Demo Dashboard   
- `minikube addons list`       
- `minikube addons enable metrics-server`
- `minikube stop`  
- `kubectl apply -f https://raw.githubusercontent.com/LianDuanTrain/K8S/main/3-Core-Concepts/springbootdemo-service-v1.yaml` 
- `minikube start`  
- `minikube dashboard`    
### Dashboard UI  
- Navigation
- Admin Overview
- Workloads
- Services
- Storage
- Config Maps and Secrets
- Logs viewer