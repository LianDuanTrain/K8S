# Ingress 
## Topics         
- How to exposing applications in Kubernetes? 
- What is Kubernetes Ingress?
- How to create a Ingress?
### How to exposing applications in Kubernetes?
- Ingress
  - Nginx Ingress 
  - HAproxy Ingress
- Dev Env
  - ClusterIP
  - NodePort
- Cloud provider
  - LoadBalancer
### What is Kubernetes Ingress?
Kubernetes Ingress is an API object that provides routing rules to manage external users' access to the services in a Kubernetes cluster. 

An API object that manages external access to the services in a cluster, typically HTTP.
Ingress may provide load balancing, SSL termination and name-based virtual hosting.

In Kubernetes, an Ingress is an object that allows access to your Kubernetes services from outside the Kubernetes cluster. You configure access by creating a collection of rules that define which inbound connections reach which services.
This lets you consolidate your routing rules into a single resource. For example, you might want to send requests to example.com/api/v1/ to an api-v1 service, and requests to example.com/api/v2/ to the api-v2 service. With an Ingress, you can easily set this up without creating a bunch of LoadBalancers or exposing each service on the Node.
https://matthewpalmer.net/kubernetes-app-developer/articles/kubernetes-ingress-guide-nginx-example.html




https://kubernetes.io/docs/concepts/services-networking/ingress/


### How to create a Ingress?
- `minikube addons enable ingress`  
- `minikube ip`  
- ```sudo echo '${minikube ip} springbootdemo.com' >> /etc/hosts```
- `minikube stop`  
- `minikube start`
- Go through YAML file 
- `kubectl apply -f ` 
- Check ingress development type
  - `kubectl get deployment -n kube-system`  
  - `kubectl  describe deployments   ingress-nginx-controller -n kube-system`  

- curl springbootdemo.com
- curl springbootdemo.com/sys
  

https://matthewpalmer.net/kubernetes-app-developer/articles/kubernetes-ingress-guide-nginx-example.html