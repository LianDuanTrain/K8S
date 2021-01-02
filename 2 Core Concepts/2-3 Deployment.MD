# Deployments
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/deploy-256.png?raw=true" width="50">  

## What is  Deployment?  
- A Deployment provides declarative updates for Pods and ReplicaSets.
- Deployment provides a management method for Pod and ReplicaSet. 
- Each Deployment corresponds to a deployment in the cluster.  
  
## How to create Deployment?
-  `kubectl run nginx-app-demo --image=nginx:1.7.9 --port=80 --replicas=3 `  
-  `kubectl apply -f https://k8s.io/examples/controllers/nginx-deployment.yaml` 


## How Deployment Controller works?
- Deployment Changes 
- ReplicaSet changes related to Deployment
- When the number of Pods related to Deployment is 0, the Pod deletion event

## How to rollling update?

<div style="background-color: white;"><image src="https://d33wubrfki0l68.cloudfront.net/30f75140a581110443397192d70a4cdb37df7bfc/fa906/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates1.svg" width="50%" Alert=""></dev>


<div style="background-color: white;"><image src="https://d33wubrfki0l68.cloudfront.net/678bcc3281bfcc588e87c73ffdc73c7a8380aca9/703a2/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates2.svg" width="50%" Alert=""></dev>


<div style="background-color: white;"><image src="https://d33wubrfki0l68.cloudfront.net/9b57c000ea41aca21842da9e1d596cf22f1b9561/91786/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates3.svg" width="50%" Alert=""></dev>


<div style="background-color: white;"><image src="https://d33wubrfki0l68.cloudfront.net/6d8bc1ebb4dc67051242bc828d3ae849dbeedb93/fbfa8/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates4.svg" width="50%" Alert=""></dev>   

https://kubernetes.io/docs/tutorials/kubernetes-basics/update/update-intro/

https://kubernetes.io/docs/concepts/workloads/controllers/deployment/

https://draveness.me/kubernetes-deployment/

https://kubernetes.io/zh/docs/concepts/workloads/controllers/deployment/