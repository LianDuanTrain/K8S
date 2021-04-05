# Dashboard  
Topic: 
- What is Dashboard?
- Demo Dashboard  

## What is Dashboard?  
- In previous classes, we learned pod, replicaset, deployment,  service, configmap, and secrets.
- I did above resources   via command line interface kubectl in live demo.    
- K8s privode Web-based user interface, K8s Dashboard to magaer all resource.   
- Dashboard deploys with a minimal RBAC configuration by default
- Dashboard Supports logging in with a Bearer Token, in minikube user proxy open a dashboard in your def brower.
  
## Demo Dashboard
let me start demo, 
first, check minikube addons
seconds, enable metrics-server - is an aggregator of resource usage data in K8S
And then, restart minikube
Next, create we learned k8s resource - pod, replicaset, deployment,  service, configmap, and secrets
Latest, start dashboard.


### Dashboard UI
the UI has three parts
top: namespace select
left: navigation menu
right: resource content  

- Navigation
- Admin Overview
- Workloads
- Services
- Storage
- Config Maps and Secrets
- Logs viewer