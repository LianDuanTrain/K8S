# Ingress 
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/ing-256.png?raw=true" width="50">  

## Topics         
- How to expos applications in Kubernetes? 
- What is Kubernetes Ingress?
- Create a Nginx Ingress
  
### How to expos applications in Kubernetes?
- Kubernetes Ingress
  - Nginx Ingress 
  - HAproxy Ingress
- Service Mesh
  - Traefik
  - Envoy
  - Istio 
- Dev Env
  - ClusterIP
  - NodePort
- Cloud provider
  - LoadBalancer
### What is Nginx Ingress?
Kubernetes Ingress is an API object that provides routing rules to manage external users' access to the services in a Kubernetes cluster.   
For Example:  
springbootdemo.com => springbootdemo service 


There are two Development Types
- DaemonSets  
- Deployments  

Logic Flow   
<image src ="https://www.nginx.com/wp-content/uploads/2020/04/NGINX-Plus-Ingress-Controller-1-7-0_ecosystem.png" width="70%">

### Create a Nginx Ingress
springbootdemo.com => springbootdemo service  
- `minikube addons enable ingress`  
- `minikube ip`  
- ```
  sudo sh -c "echo '$(minikube ip) springbootdemo.com' >> /etc/hosts"
  cat   /etc/hosts
  ```
- `minikube stop`  
- `minikube start`
- Go through YAML file 
- `kubectl apply -f https://raw.githubusercontent.com/LianDuanTrain/K8S/main/4-Adavance/springboot-demo-service-v1.yaml`   
- `kubectl apply -f https://raw.githubusercontent.com/LianDuanTrain/K8S/main/4-Adavance/ingress-demo-v1.yaml`  
- Check ingress development type
  - `kubectl get deployment -n kube-system`  
  - `kubectl  describe deployments   ingress-nginx-controller -n kube-system`  
- Test springbootdemo
  - curl springbootdemo.com
  - curl springbootdemo.com/sys|jq
- `kubectl delete -f https://raw.githubusercontent.com/LianDuanTrain/K8S/main/4-Adavance/ingress-demo-v1.yaml`  
  
 

  
