
# Blue/Green Deployment
## Topics
- What is Blue/Green Deployment?
- Demo  
  - Create Blue Deployment and Ingress
  - Create Green Deployment and Ingress
  - Switch network traffic from Blue to Green

## What is Blue/Green Deployment?
- A Blue/Green deployment is a way of accomplishing a zero-downtime upgrade to an - existing application. 
- The “Blue” version is the currently running copy of the application T
he “Green” version is the new version. 
- Once the green version is ready, traffic is rerouted to the new version.


## Demo  
<image src ="greenblue.gif" width="70%">  

### Create a Blue Deployment
#### www.springbootdemo.com => springbootdemo-v1 service  
- `minikube addons enable ingress`  
- `minikube ip`  
- ```
  sudo sh -c "echo '$(minikube ip) www.springbootdemo.com' >> /etc/hosts"
  cat   /etc/hosts
  ```
- Deployment 
  - metadata => version: v1
- Pod   
  - metadata => version: v1
- Service
  - selector => version: v1

- `kubectl apply -f https://github.com/LianDuanTrain/K8S/blob/main/4-Adavance/Blue%20Green%20Deployment%20Yaml/springboot-demo-service-blue-v1.yaml`  

#### Test Service
  - `kubectl run  -it busybox --rm --image=yauritux/busybox-curl --restart=Never -n k8s-training -- sh -ls` 
  - `curl www.springbootdemo-v1`

### Create a Blue Ingress
  - service => name: springbootdemo-v1  
  - `kubectl apply -f https://github.com/LianDuanTrain/K8S/blob/main/4-Adavance/Blue%20Green%20Deployment%20Yaml/blue-ingress-demo.yaml`    
#### Test Blue Ingress
  - curl www.springbootdemo.com
  - curl www.springbootdemo.com/sys|jq

### Create a Green Deployment
#### test.springbootdemo.com => springbootdemo-v2 service   
- `minikube ip`  
- ```
  sudo sh -c "echo '$(minikube ip) test.springbootdemo.com' >> /etc/hosts"
  cat   /etc/hosts
  ```
- Deployment 
  - metadata => version: v2
- Pod   
  - metadata => version: v2
- Service
  - selector => version: v2

  
- `kubectl apply -f https://github.com/LianDuanTrain/K8S/blob/main/4-Adavance/Blue%20Green%20Deployment%20Yaml/springboot-demo-service-blue-v1.yaml`  

#### Test Service
  - `kubectl run  -it busybox --rm --image=yauritux/busybox-curl --restart=Never -n k8s-training -- sh -ls` 
  - `curl test.springbootdemo-v2`

### Create a Green Ingress
  - service => name: springbootdemo-v2
  - `kubectl apply -f https://github.com/LianDuanTrain/K8S/blob/main/4-Adavance/Blue%20Green%20Deployment%20Yaml/green-ingress-demo.yaml`   
#### Test Green Ingress
  - curl test.springbootdemo.com
  - curl test.springbootdemo.com/sys|jq  
  
### Switch Network Traffic from Blue to Green

- `kubectl patch ing/blue-ingress-demo --type=json -p='[{"op": "replace", "path": "/spec/rules/0/http/paths/0/backend/serviceName", "value":"springbootdemo-v2"}]' -n k8s-training` 
- `kubectl delete ingress blue-ingress-demo -n k8s-training`     

