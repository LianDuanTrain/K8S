Welcome to our class. Today we will learn 
## What is Deployment?  
## How to create Deployment?
## What is trigger of Deployment Controller?
## How to scale deployment?


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

The kubectl is balt to create a pod as above yaml file
- Alternative way    
   -  `kubectl run nginx-deployment --image=nginx:1.14.2 --port=80 --replicas=3 `    

# How to scale deployment?

## What is trigger of Deployment Controller?
Deployment implement is Deployment Controller.
- Deployment changes will triage  Deployment Controller, such as docker image version update
- ReplicaSet increase or decrease will triage Deployment Controller. 
- Pods are deleted when the number of Pods related to Deployment is 0



####################################################################
Today we leaned Kubernetes core concepts - Deployment.
Deployment definition 
Create Deployment in two ways
Scale deployment?
Three triggers of Deployment Controller


- `kubectl get deployment springbootdemo-deployment -o yaml`  
- `kubectl get pods`
- `kubectl get replicasets`
- `kubectl get deployments`
- `kubectl get events --sort-by=.metadata.creationTimestamp`



Thank you for watching, see you in the next class.




