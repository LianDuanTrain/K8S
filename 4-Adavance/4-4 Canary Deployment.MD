
# Canary Deployment
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/ing-256.png?raw=true" width="50"> 

## Topics
- What is Canary Deployment?
- How to implement Canary Deployment with Ingress?
- Demo  

# What is Canary Deployment?

- App v1    
<image src="Canary Deployment0.png" width="50%"/>  
- App v1 and App v2   
<image src="Canary Deployment.png" width="50%"/>  

- A canary deployment
- Roll out new code to a subset of users as an initial test.  
# How to implement Canary Deployment with Nginx Ingress?
- Customization Ingress Resource
  - enable Ingress addons
  - enable canary in Ingress Resource
- Canary Type
  - header
  - cookie
  - weight
  - Canary rules are evaluated in order of precedence
   - canary-by-header -> canary-by-cookie -> canary-weight
# Demo 
- `minikube addons enable ingress`  
- `minikube ip`  
- ```
  sudo sh -c "echo '$(minikube ip) springbootdemo.com' >> /etc/hosts"
  cat   /etc/hosts
  ```  

## APPs
### V1 
- Go through YAML file
- `kubectl apply -f https://raw.githubusercontent.com/LianDuanTrain/K8S/main/4-Adavance/Canary%20Deployment%20Yaml/springboot-demo-service-v1.yaml`

  - Deployment
    - springbootdemo-deployment-v1
  - Pod   
    - springbootdemo-v1 
  - Service
    - springbootdemo-service-v1 
- Check resource    
  - `kubectl get all -n k8s-trainin`
### Ingress
- www.springbootdemo.com - > springbootdemo-service-v1 
- Go through YAML file
- `kubectl apply -f https://raw.githubusercontent.com/LianDuanTrain/K8S/main/4-Adavance/Canary%20Deployment%20Yaml/ingress-v1.yaml`
- `kubectl describe ingress ingress-v1 --namespace=k8s-training`
- `curl www.springbootdemo.com`   
### V2 
- Go through YAML file
- `kubectl apply -f https://raw.githubusercontent.com/LianDuanTrain/K8S/main/4-Adavance/Canary%20Deployment%20Yaml/springboot-demo-service-v2.yaml`

- Deployment
  - springbootdemo-deployment-v2
- Pod   
  - springbootdemo-v2  
- Service
  - springbootdemo-service-v2 

## Weight Ingress
- Go through YAML file
- `kubectl apply -f https://raw.githubusercontent.com/LianDuanTrain/K8S/main/4-Adavance/Canary%20Deployment%20Yaml/canary-weight-ingress.yaml`
  - nginx.ingress.kubernetes.io/canary: "true"
  - nginx.ingress.kubernetes.io/canary-weight: "50"
- `curl www.springbootdemo.com`    
## Header Ingress
- `kubectl apply -f https://raw.githubusercontent.com/LianDuanTrain/K8S/main/4-Adavance/Canary%20Deployment%20Yaml/canary-by-header-ingres.yaml`
  - nginx.ingress.kubernetes.io/canary: "true"
  - nginx.ingress.kubernetes.io/canary-by-header: "Region"
  - nginx.ingress.kubernetes.io/canary-by-header-pattern: "VA|MD"
- `curl www.springbootdemo.com`  

