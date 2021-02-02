# Deployment
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/deploy-256.png?raw=true" width="50">  

## What is Deployment?  
- Deployment provides a management method for Pod and ReplicaSet.  
  
## How to create Deployment?
-  `kubectl apply -f springbootdemo-deployment.yaml` 
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
```
- Alternative way    
   
   - kubectl run --generator=deployment/v1 springbootdemo-deployment --image=lianduantraining/springbootdemo:v1 --port=9999
  
- `kubectl get deployment springbootdemo-deployment -o yaml`  
- `kubectl get pods`
- `kubectl get replicasets`
- `kubectl get deployments`
- `kubectl get events --sort-by=.metadata.creationTimestamp`



<img src='image\Deployment.jpg'>

## How to scale deployment? 

- `kubectl scale deployment/springbootdemo-deployment --replicas=3 -record=true`
- After 1.18.0    
  ~~kubectl run --generator=deployment/v1 springbootdemo-deployment --image=lianduantraining/springbootdemo:v1 --port=9999 --replicas=3~~ 
  

## What is trigger of Deployment Controller?
- Deployment changes 
- ReplicaSet changes related to Deployment
- When the number of Pods related to Deployment is 0, the Pod deletion event triage

