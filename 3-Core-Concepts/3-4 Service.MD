# Service
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/svc-256.png?raw=true" width="50">   

## What is service?
- An abstract way to expose an application running on a set of Pods as a network service.
- ServiceTypes 
  - ClusterIP
  - NodePort
  - LoadBalancer
  - ExternalName

## How to create a Service?
- `kubectl apply -f springbootdemo-service.yaml`
```
# API Version  
apiVersion: apps/v1
kind: Deployment
# Deployment metadata start
metadata:
  name: springbootdemo-deployment
  labels:
    app: springbootdemo
# Deployment metadata end
# Pod spec start    
spec:
  replicas: 1
  selector:
    matchLabels:
      app: springbootdemo
# Pod spec end       
# template start      
  template:
    metadata:
      labels:
        app: springbootdemo
    spec:
      containers:
      - name: springbootdemo
        image: lianduantraining/springbootdemo:v1
        ports:
        - containerPort: 9999
# template end 
---
apiVersion: v1
kind: Service
metadata:
  name: springbootdemo
spec:
  selector:
    app: springbootdemo
  ports:
    - protocol: TCP
      port: 9999
      targetPort: 9999
```
- Check Service
  - `kubectl get svc` 
  - `kubectl get endpoints` 
  - `kubectl get pods`
  - `kubectl logs springbootdemo-deployment-XXX`  
  - `kubectl scale deployment/springbootdemo-deployment --replicas=3  --record=true`
  - `kubectl get endpoints`
- Access Springbootdemo 
  - `kubectl run  -it busybox --rm --image=yauritux/busybox-curl --restart=Never -- sh`     
    - `curl X.X.X.X:9999`  

## Why need service?
- Service discovery without modify application 
  -  Environment variables
     - `kubectl get pods`   
     - `kubectl exec -it  springbootdemo-deployment-XXX -- env`  
  -  DNS
     - busybox
       - `kubectl run  -it busybox --rm --image=busybox:1.28.4 --restart=Never -- sh`
       - `nslookup springbootdemo`
       - `wget springbootdemo:9999`
     - K8S dnsutils
       - `kubectl apply -f https://k8s.io/examples/admin/dns/dnsutils.yaml`
       - `kubectl exec -it dnsutils -- nslookup springbootdemo`  
       - `kubectl exec -it dnsutils -- wget springbootdemo:9999`    
       - `kubectl exec -it dnsutils -- cat  index.html` 
  
- Access point for group of pods

## Service Load-Balance Types
-  User space proxy mode
-  Iptables proxy mode
-  IPVS proxy mode
###  Check Load-Balance Types
   - `kubectl get -n kube-system configmap kube-proxy -o yaml`
   - `minikube ssh`
     - `grep -e ipvs -e nf_conntrack_ipv4 /lib/modules/$(uname -r)/modules.builtin`  
     - `sudo iptables -t nat -L KUBE-SERVICES -n |grep springbootdemo`









