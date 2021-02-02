Welcome to our class. Today we will learn 
## What is Deployment?  
## How to create Deployment?
## What is trigger of Deployment Controller?
## How to rollling update?


<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/deploy-256.png?raw=true" width="50">  

## What is Deployment?  
- Deployment provides a management method for Pod and ReplicaSet. 
- Kubernetes is a declarative system (by opposition to imperative systems). This means that I can’t give it orders. I can’t say, “run this container.” All I can do, is describe what I want to have, and wait for Kubernetes to take action to reconcile what I have, with what I want to have.
- Deployment is a declarative

  
## How to create Deployment?
-  `kubectl apply -f springbootdemo-deployment.yaml` 

The yaml file has three part
First , API version
Second, Deployment metadata, the metadata has name and labels, the lable for service selected.
Latest, Pod, pod includes two parts, spec and pod template. 
Spec has selector and template. the value should be match. 

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
  replicas: 3
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
```
```
The kubectl is balt to create a pod as above yaml file
- Alternative way    
   -  `kubectl run nginx-deployment --image=nginx:1.14.2 --port=80 --replicas=3 `    

## What is trigger of Deployment Controller?
Deployment implement is Deployment Controller.
- Deployment changes will triage  Deployment Controller, such as docker image version update
- ReplicaSet increase or decrease will triage Deployment Controller. 
- Pods are deleted when the number of Pods related to Deployment is 0

## How to rollling update?
There are three pods and four apps v1, the color is light green
### Init  
<div style="background-color: lightgray;" width=500px><image src="https://d33wubrfki0l68.cloudfront.net/30f75140a581110443397192d70a4cdb37df7bfc/fa906/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates1.svg" width=50% Alert="Figure 1"></div>  

Start one apps v2, the color is purple.

### Update Start
<div style="background-color: lightgray;"><image src="https://d33wubrfki0l68.cloudfront.net/678bcc3281bfcc588e87c73ffdc73c7a8380aca9/703a2/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates2.svg" width="50%" Alert="Figure 2"></div>

Start second apps v2, and delete two app v1.

### Update  Peocess
<div style="background-color: lightgray;"><image src="https://d33wubrfki0l68.cloudfront.net/9b57c000ea41aca21842da9e1d596cf22f1b9561/91786/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates3.svg" width="50%" Alert="Figure 3"></div>

Update completed. start thrid and fourth app v2, and delete ramaining appv1

### Update Finish
<div style="background-color: lightgray;"><image src="https://d33wubrfki0l68.cloudfront.net/6d8bc1ebb4dc67051242bc828d3ae849dbeedb93/fbfa8/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates4.svg" width="50%" Alert="Figure 4"></div>   


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

