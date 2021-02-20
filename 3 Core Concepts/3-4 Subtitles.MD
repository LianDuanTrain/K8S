Welcome to our class. Today we will learn 
## What is service?
## How to create a Service?
## Why need service?
## Service Load-Balance Types



# Service
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/svc-256.png?raw=true" width="50">   

## What is service?
- Service access point of a group of Pods.  
- Service has four Types 
  - ClusterIP is default service type. Cluster IP is internal IP for cluster. Can not access outside.
  - NodePort, export port of Node. I can access  my app on the port from outside. It usually for debugging app in dev env. the port range is from 30000-32767. 
  - LoadBalancer, your clould service will provider LoadBalancer.
  - ExternalName, expose server via DNS name.
  
## How to create a Service?
the yaml file has two part and splilte by ---
first part is used create a pod, the content is same as we deployment class. You can go to my  deployment to get all detail.
Second part is used to create service

First session API defance .
apiVersion: v1
kind: Service
metadata.

Second session is spec.
selector is used to select pods which have  metadata, name: springbootdemo.  
ports, 
protocol is tcp, 
source port is 9999, 
targetPort is Pod port, the number is 9999.

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
Let me un the command 
the command create two resource, a service resource and endpoint resource. Let me check. endpoint has service and pod mapping info.

- Check Service
  - `kubectl get svc`  get service list
  - `kubectl get endpoints`   get endpoints list, 
  - `kubectl get pods`  
  - `kubectl logs springbootdemo-deployment-XXX`  to check the pod log to make sure the pod is working 
  -  there is only one pod, if replicas pod to 3 endpoints info will change. 
  - `kubectl scale deployment/springbootdemo-deployment --replicas=3  --record=true`
  - `kubectl get endpoints` 
- Access Springbootdemo 
  - `kubectl run  -it busybox --rm --image=yauritux/busybox-curl --restart=Never -- sh`   let me start a pod to access the  springbootdemo. The command is   . The pod is based on   busybox-curl image. the image add curl command on  busybox image because the origianl busybox does not have curl command.
    - `curl X.X.X.X:9999` 
 

## Why need service?
- K8s provide Service discovery function without modify application. The server registry cneter does not need. The servers are able to access eacth other via service name. There are two ways are able to find service name.
  -  Environment variables - when the pod is created the Environment variables was added. The Environment variables does not support hot update.
     - `kubectl get pods`   
     - `kubectl exec -it springbootdemo-deployment-XXX -- env`  
  -  DNS - app can use service name to access each other, core dns pod privode DNS service.  
     - Check core dns
       -`kubectl get pods --namespace=kube-system -l k8s-app=kube-dns`  
       -`kubectl get svc --namespace=kube-system`  
     - next , lunch a busybox pod to access springbootdemo service
       - `kubectl run  -it busybox --rm --image=busybox:1.28.4 --restart=Never -- sh`
       - `nslookup springbootdemo`
       - `wget springbootdemo:9999`
     - also K8S private dnsutils image to check core dns service 
       - `kubectl apply -f https://k8s.io/examples/admin/dns/dnsutils.yaml`
       - `kubectl exec -it dnsutils -- nslookup springbootdemo`  
       - `kubectl exec -it dnsutils -- wget springbootdemo:9999`    
       - `kubectl exec -it dnsutils -- cat  index.html`  

- Pods are nonpermanent resources. Each Pod gets its own IP address so need a access point for group of pods.

## Service Load-Balance Types 
kube-proxy is used to Load-Balance outside or inside network trafic to service. kube-proxy could run as thread or daemonset service on each work node.
-  User space proxy mode - the mode is deprecate
-  Iptables proxy mode
   IPTABLES mode was added in v1.1 and became the default operation mode since v1.2
   In this mode, kube-proxy watches the Kubernetes control plane for the addition and removal of Service and Endpoint objects. For each Service, it installs iptables rules, which capture traffic to the Service's clusterIP and port, and redirect that traffic to one of the Service's backend sets. 
   This is default proxy mode
   If the K8s cluster huge, maintation iptables is nignmare and couse performance issue.   
- IPVS proxy mode
  IPVS mode was introduced in Kubernetes v1.8  
  Both IPVS and IPTABLES are based on linux core - netfilter. 
  The differences between IPVS mode and IPTABLES mode are as follows:
    IPVS provides better scalability and performance for large clusters.
    IPVS supports more complex load balancing algorithms (minimum load, minimum connections, location, weighting, etc.) than iptables.
    IPVS supports server health check and connection retry.
### Check Load-Balance Types
   - `kubectl get -n kube-system configmap kube-proxy -o yaml`
   - `minikube ssh`
     - `grep -e ipvs -e nf_conntrack_ipv4 /lib/modules/$(uname -r)/modules.builtin`  
     - `sudo iptables -t nat -L KUBE-SERVICES -n |grep springbootdemo`

In a production environment, CNI plugins, such as Flannel、Calico were used. because they have more manageable network traffic and high performance then kube-proxy.

####################################################################
Today we leaned Kubernetes core concepts - service.
Service definition and four service types
How to create a service via yaml file.
Service Load-balance types

Thank you for watching, see you in the next class.


