# Ingress 
## Topics         
- Four ways exposing applications deployed in Kubernetes 
- What is Kubernetes Ingress?
- What is the Ingress Controller?
- How to create a Ingress?
### Four ways exposing applications deployed in Kubernetes
- Ingress 
- ClusterIP
- NodePort
- LoadBalancer
### What is Kubernetes Ingress?
In Kubernetes, an Ingress is an object that allows access to your Kubernetes services from outside the Kubernetes cluster. You configure access by creating a collection of rules that define which inbound connections reach which services.
This lets you consolidate your routing rules into a single resource. For example, you might want to send requests to example.com/api/v1/ to an api-v1 service, and requests to example.com/api/v2/ to the api-v2 service. With an Ingress, you can easily set this up without creating a bunch of LoadBalancers or exposing each service on the Node.
https://matthewpalmer.net/kubernetes-app-developer/articles/kubernetes-ingress-guide-nginx-example.html

### What is the Ingress Controller?
An API object that manages external access to the services in a cluster, typically HTTP.
Ingress may provide load balancing, SSL termination and name-based virtual hosting.

https://kubernetes.io/docs/concepts/services-networking/ingress/


### How to Use Nginx Ingress Controller?
- Installation Guide
- Creating a Kubernetes Ingress

https://matthewpalmer.net/kubernetes-app-developer/articles/kubernetes-ingress-guide-nginx-example.html