Welcome to our class. Today we will learn 
## What is Deployment?  
## How to create Deployment?
## What is trigger of Deployment Controller?
## How to rollling update?


# Deployment
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/deploy-256.png?raw=true" width="50">  

## What is Deployment?  
- A Deployment provides declarative updates for Pods and ReplicaSets.
- Deployment provides a management method for Pod and ReplicaSet. 
- Each Deployment corresponds to a deployment in the cluster.  
  
## How to create Deployment?
-  `kubectl apply -f https://k8s.io/examples/controllers/nginx-deployment.yaml` 
  ```
# API Version  
apiVersion: apps/v1
kind: Deployment
# Deployment metadata start
metadata:
  name: nginx-deployment
  labels:
    app: nginx
# Deployment metadata end
# Pod spec start    
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
# Pod spec end       
# template start      
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
# template end ```
- Alternative way    
   -  `kubectl run nginx-deployment --image=nginx:1.14.2 --port=80 --replicas=3 `    

## What is trigger of Deployment Controller?
- Deployment Changes 
- ReplicaSet changes related to Deployment
- When the number of Pods related to Deployment is 0, the Pod deletion event

## How to rollling update?
In Kubernetes, this is done with rolling updates. 
Rolling updates allow Deployments' updates to take place with zero downtime.
The new Pods will be scheduled on Nodes with available resources.
One sentence for Rolling updates, Increase new pods and  reduce old pods .

### Init  
There are three pods and four addps. 
<div style="background-color: lightgray;" width=500px><image src="https://d33wubrfki0l68.cloudfront.net/30f75140a581110443397192d70a4cdb37df7bfc/fa906/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates1.svg" width=50% Alert="Figure 1"></div>  

### Update Start
<div style="background-color: white;"><image src="https://d33wubrfki0l68.cloudfront.net/678bcc3281bfcc588e87c73ffdc73c7a8380aca9/703a2/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates2.svg" width="50%" Alert="Figure 2"></div>

### Update  Peocess
<div style="background-color: white;"><image src="https://d33wubrfki0l68.cloudfront.net/9b57c000ea41aca21842da9e1d596cf22f1b9561/91786/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates3.svg" width="50%" Alert="Figure 3"></div>

### Update Finish
<div style="background-color: white;"><image src="https://d33wubrfki0l68.cloudfront.net/6d8bc1ebb4dc67051242bc828d3ae849dbeedb93/fbfa8/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates4.svg" width="50%" Alert="Figure 4"></div>   

https://kubernetes.io/docs/tutorials/kubernetes-basics/update/update-intro/

https://kubernetes.io/docs/concepts/workloads/controllers/deployment/

https://draveness.me/kubernetes-deployment/

https://kubernetes.io/zh/docs/concepts/workloads/controllers/deployment/

Figure 1.  
Source:(https://d33wubrfki0l68.cloudfront.net/30f75140a581110443397192d70a4cdb37df7bfc/fa906/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates1.svg)
Figure 2.  
Source:(https://d33wubrfki0l68.cloudfront.net/678bcc3281bfcc588e87c73ffdc73c7a8380aca9/703a2/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates2.svg)
Figure 3.  
Source:(https://d33wubrfki0l68.cloudfront.net/678bcc3281bfcc588e87c73ffdc73c7a8380aca9/703a2/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates3.svg)
Figure 4.  
Source:(https://d33wubrfki0l68.cloudfront.net/678bcc3281bfcc588e87c73ffdc73c7a8380aca9/703a2/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates4.svg)

####################################################################
Today we leaned Kubernetes core concepts - Deployment.
Deployment definition?  
Create Deployment in two ways
Three triggers of Deployment Controller
Rollling update process.



Thank you for watching, see you in the next class.


Figure 1. Pods overview 
Source:(https://d33wubrfki0l68.cloudfront.net/fe03f68d8ede9815184852ca2a4fd30325e5d15a/98064/docs/tutorials/kubernetes-basics/public/images/module_03_pods.svg)

