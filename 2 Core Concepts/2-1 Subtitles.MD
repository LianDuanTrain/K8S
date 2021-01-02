Welcome to our class. Today we learn K8s Pod. There are three topics.
 What is Pod?
 How to use Pod?
 What is Pod templates?

# Pod 
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/pod-256.png?raw=true" width="50
">

## What is Pod?
- Pods are the atomic unit on the Kubernetes platform.
- When we create a Deployment on Kubernetes, that Deployment creates Pods with containers inside them.
- A Pod models an application-specific "logical host" and can contain different application containers which are relatively tightly coupled. While , the best practice is deploy one application on one pod becasue when the  application overload, we can easy scale it. If five apps  deploy to one pod, one of five have overload, we have to deploy five apps.
-  The pod is attached to the node. The node may fail. The controller of kubernetes such as the replication will start a pod on other nodes, and the new pod will be assigned a new IP;

- Shared resources for containers
  - Containers can share Storage, such as volume
  - Networking, as a unique cluster IP address. container access each other via localhost
  - Information about how to run each container. such as the container image version or specific ports to use.

<div style="background-color: lightgray;"><img  src ='https://d33wubrfki0l68.cloudfront.net/fe03f68d8ede9815184852ca2a4fd30325e5d15a/98064/docs/tutorials/kubernetes-basics/public/images/module_03_pods.svg' ></div>

## How to use Pod?
- Pods  run a single container  
- Pods  run multiple containers that need to work together
- Pods are created/managed by Workload resources  
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


####################################################################
Today we leaned Kubernetes core concepts - pod.
Pods are the atomic unit on the Kubernetes platform.
Pods  run a single/multiple container
Pods are created/managed by Workload resources

Thank you for watching, see you in the next class.


Figure 1. Pods overview 
Source:(https://d33wubrfki0l68.cloudfront.net/fe03f68d8ede9815184852ca2a4fd30325e5d15a/98064/docs/tutorials/kubernetes-basics/public/images/module_03_pods.svg)

