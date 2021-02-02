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
   - After 1.18.0~~kubectl run --generator=deployment/v1beta1 nginx-deployment --image=nginx:1.14.2 --port=80 --replicas=3~~   
 -  
- `kubectl get deployment springbootdemo-deployment -o yaml`  
- `kubectl get pods`
- `kubectl get replicasets`
- `kubectl get deployments`
- `kubectl get events --sort-by=.metadata.creationTimestamp`



<img src='image\Deployment.jpg'>

## How to scale deployment? 

- `kubectl scale deployment/springbootdemo-deployment --replicas=3 -record=true`
  

## What is trigger of Deployment Controller?
- Deployment changes 
- ReplicaSet changes related to Deployment
- When the number of Pods related to Deployment is 0, the Pod deletion event triage

## How to rollling update?
### Init  
<div style="background-color: lightgray;" width=500px><image src="https://d33wubrfki0l68.cloudfront.net/30f75140a581110443397192d70a4cdb37df7bfc/fa906/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates1.svg" width=50% Alert="Figure 1"></div>  

### Update Start
<div style="background-color: lightgray;"><image src="https://d33wubrfki0l68.cloudfront.net/678bcc3281bfcc588e87c73ffdc73c7a8380aca9/703a2/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates2.svg" width="50%" Alert="Figure 2"></div>

### Update  Peocess
<div style="background-color: lightgray;"><image src="https://d33wubrfki0l68.cloudfront.net/9b57c000ea41aca21842da9e1d596cf22f1b9561/91786/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates3.svg" width="50%" Alert="Figure 3"></div>

### Update Finish
<div style="background-color: lightgray;"><image src="https://d33wubrfki0l68.cloudfront.net/6d8bc1ebb4dc67051242bc828d3ae849dbeedb93/fbfa8/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates4.svg" width="50%" Alert="Figure 4"></div>   

`kubectl set image deployment/springbootdemo-deployment springbootdemo=lianduantraining/springbootdemo:v2`  
`kubectl rollout status deployment/springbootdemo-deployment -w`  
`kubectl rollout history deployment/springbootdemo-deployment `  
`kubectl rollout history deployment.v1.apps/springbootdemo-deployment --revision=2`  
`kubectl rollout status -w deployment/springbootdemo-deployment `   
`kubectl autoscale deployment.v1.apps/springbootdemo-deployment --min=1 --max=3 --cpu-percent=80` 









https://blog.fleeto.us/post/kubernetes-deployments-the-ultimate-guide/


Figure 1.  
Source:(https://d33wubrfki0l68.cloudfront.net/30f75140a581110443397192d70a4cdb37df7bfc/fa906/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates1.svg)   
Figure 2.  
Source:(https://d33wubrfki0l68.cloudfront.net/678bcc3281bfcc588e87c73ffdc73c7a8380aca9/703a2/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates2.svg)   
Figure 3.  
Source:(https://d33wubrfki0l68.cloudfront.net/678bcc3281bfcc588e87c73ffdc73c7a8380aca9/703a2/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates3.svg)   
Figure 4.  
Source:(https://d33wubrfki0l68.cloudfront.net/678bcc3281bfcc588e87c73ffdc73c7a8380aca9/703a2/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates4.svg)   