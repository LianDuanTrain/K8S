# Pod 
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/pod-256.png?raw=true" width="50
">

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



## What is Pod templates?
Workload resources create Pods from a pod template and manage those Pods  
```
apiVersion: batch/v1  
kind: Job
metadata:
  name: hello
spec:
  template:
    # This is the pod template
    spec:
      containers:
      - name: hello
        image: busybox
        command: ['sh', '-c', 'echo "Hello, Kubernetes!" && sleep 3600']
      restartPolicy: OnFailure
    # The pod template ends here
```


Figure 1. Pods overview 
Source:(https://d33wubrfki0l68.cloudfront.net/fe03f68d8ede9815184852ca2a4fd30325e5d15a/98064/docs/tutorials/kubernetes-basics/public/images/module_03_pods.svg)



