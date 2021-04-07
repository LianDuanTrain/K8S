# Ingress 
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/ing-256.png?raw=true" width="50">  
Welcome to our class. Today we will learn Secrets.
## Topics         
- How to expos applications in Kubernetes? 
- What is Kubernetes Ingress?
- Create a Nginx Ingress
  
### How to expos applications in Kubernetes?


- First Traditional Way (Kubernetes) Ingress
  there are lof of Ingress inplementen in marcket, such as.
  Ingress can redirected user access network tracket to service based on demon name. Uallly, the  Ingress has two versions, free version and pay verson. Couurande requements, you can chose. 
  - Nginx Ingress 
  - HAproxy Ingress
  Ingress support hot reload config file when you create new Ingress object. When you have large cluster, the hot reload will perfenerce butto nick.
- Next , Service Mesh Way 
  - Traefik
  - Envoy
  - Istio 
- And then, in Dev Env
  - we can expose ClusterIP to access a service
  - Or expose NodePort to access a service 
- Finally, Cloud provider
  - If app have static Ip, LoadBalancer is able to redirce your network tracivk to a service.


### What is Kubernetes Ingress?
Kubernetes Ingress is an API object that provides routing rules to manage external users' access to the services in a Kubernetes cluster. 

An API object that manages external access to the services in a cluster, typically HTTP.
Ingress may provide load balancing, SSL termination and name-based virtual hosting.

In Kubernetes, an Ingress is an object that allows access to your Kubernetes services from outside the Kubernetes cluster. You configure access by creating a collection of rules that define which inbound connections reach which services.
This lets you consolidate your routing rules into a single resource. For example, you might want to send requests to example.com/api/v1/ to an api-v1 service, and requests to example.com/api/v2/ to the api-v2 service. With an Ingress, you can easily set this up without creating a bunch of LoadBalancers or exposing each service on the Node.
https://matthewpalmer.net/kubernetes-app-developer/articles/kubernetes-ingress-guide-nginx-example.html




https://kubernetes.io/docs/concepts/services-networking/ingress/


### How to create a Nginx Ingress?
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
