# Ingress 

<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/ing-256.png?raw=true" width="50">  
Welcome to our class. Today we will learn Ingress.
## Topics         
- How to expos applications in Kubernetes? 
- What is Kubernetes Ingress?
- Create a Nginx Ingress
  
### How to expos applications in Kubernetes?




- First Traditional Way (Kubernetes) Ingress
Ingress can redirected user  network tracket to service based on demon name or demon+path. 
  there are lof of Ingress inplementen in marcket, such as.
    - Nginx Ingress 
  - HAproxy Ingress
 Uallly, the  Ingress inplementen has two versions, free version and pay verson. Couurande requements, you can chose. 

Ingress support hot reload config file when you create new Ingress object. When you have large cluster, the hot reload will perfenerce butto nick.

- Next , use Service Mesh to access apps
  - Traefik
  - Envoy
  - Istio 
  
- And then, in Dev Env
  - we can expose ClusterIP to access a service
  - Or expose NodePort to access a service 
- Finally, Cloud provider
  - If app has static Ip, LoadBalancer is able to redirce your network tracivk to a service.


### What is Kubernetes Ingress?
Kubernetes Ingress is an API object that provides routing rules to manage external users' access to the services in a Kubernetes cluster. 

Ingress is An API object that manages external access to the services in a cluster, typically HTTP and https
Ingress may provide load balancing, SSL termination and name-based virtual hosting.

Example:
springbootdemo.com => springbootdemo service 


There are two Development Types
- DaemonSets , the type need to deployment Nginx Ingress  to each worker node. outside LoadBalancer need to point to each k8s working node. 
- Deployments typle like regular service Deployment. only one Ingress service in K8s cluster.outside LoadBalancer only need to  point to the Ingress service. Logic Flow  as blow 

Logic Flow   
<image src ="https://www.nginx.com/wp-content/uploads/2020/04/NGINX-Plus-Ingress-Controller-1-7-0_ecosystem.png" width="70%">

let's run a demo
### Create a Nginx Ingress
First enable ingress
- `minikube addons enable ingress`  
  Next get minikube ip
- `minikube ip`  
  And then, add demon name and Ip to hosts file because the demon name is not real demon name.
- ```
  sudo sh -c "echo '$(minikube ip) springbootdemo.com' >> /etc/hosts"
  cat   /etc/hosts
  ```
Next restart minikune service  
- `minikube stop`  
- `minikube start`
- Go through YAML file 
- `kubectl apply -f https://raw.githubusercontent.com/LianDuanTrain/K8S/main/4-Adavance/springboot-demo-service-v1.yaml`   
- `kubectl apply -f https://raw.githubusercontent.com/LianDuanTrain/K8S/main/4-Adavance/ingress-demo-v1.yaml`  
the file has three parts api, metadata, spec
Next step,
- Check ingress development type
  - `kubectl get deployment -n kube-system`  
  - `kubectl  describe deployments   ingress-nginx-controller -n kube-system`  
- Test springbootdemo
  - curl springbootdemo.com
  - curl springbootdemo.com/sys|jq
- `kubectl delete -f https://raw.githubusercontent.com/LianDuanTrain/K8S/main/4-Adavance/ingress-demo-v1.yaml`  

####################################################################
Today we leaned Kubernetes Ingress 

- How to expos applications in Kubernetes? 
- What is Kubernetes Ingress?
- Create a Nginx Ingress

Thank you for watching, see you in the next class.
  