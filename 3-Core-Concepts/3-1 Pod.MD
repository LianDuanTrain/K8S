# Pod 
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/pod-256.png?raw=true" width="50">

## What is Pod?
- Pods are the smallest deployable units in Kubernetes.
- A Pod is a group of one or more containers.
- A Pod models an application-specific "logical host"
- A Pod is attached to the node.
- Shared resources for containers
  - Storage
  - Networking, as a unique cluster IP address
  - Information about how to run each container
 
<div style="background-color: lightgray;"><img  src ='https://d33wubrfki0l68.cloudfront.net/fe03f68d8ede9815184852ca2a4fd30325e5d15a/98064/docs/tutorials/kubernetes-basics/public/images/module_03_pods.svg' ></div> 

  

## How to use Pod?
- Pods run a single container  
- Pods run multiple containers that need to work together
- Pods are created/managed by workload resources  
   - Deployment
   - StatefulSet
   - DaemonSet

### Demo
- `kubectl create deployment mynginx --image=nginx:1.19-alpine`
   -  https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create 
- `kubectl get pod`   
- `kubectl get pod -o wide`
- kubectl [command] [TYPE] [NAME] [flags]

## What is Pod template?
Workload resources create Pods from a pod template and manage those Pods  
```
apiVersion: apps/v1  
kind: Deployment
metadata:
  name: mynginx
spec:
  template:
    # This is the pod template start
    spec:
      containers:
      - name: mynginx
        image: nginx:1.19-alpine
    # The pod template ends here
```


Figure 1. Pods overview 
Source:(https://d33wubrfki0l68.cloudfront.net/fe03f68d8ede9815184852ca2a4fd30325e5d15a/98064/docs/tutorials/kubernetes-basics/public/images/module_03_pods.svg)



