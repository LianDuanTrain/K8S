Welcome to our class. Today we fource on ReplicaSet.
 What is ReplicaSet?
 How a ReplicaSet works?
 When  using a ReplicaSet?

<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/rs-256.png?raw=true" width="50">  

## What is ReplicaSet?
- A ReplicaSet purpose is creating and deleting Pods as needed to reach the desired number.  Also called Self-healing
- .
- When a ReplicaSet needs to create new Pods, it uses its Pod template.
  ReplicaSet implement by Replicaset Controller is a daemon that runs in never ending loop.


## How a ReplicaSet works?
There is a example, the K8s cluster has one master node and two work nodes. App1 ReplicaSet value is two. K8s will start two pod in each node. each pos has one app1 so there are total two app1 in the k8s cluster. Eatch 10 seconds, node report pod status to etcd.
- ReplicaSet = 2, one App1 is on Note A and one App1 is on Note B
<image src ="image/ReplicaSet1.jpg" width=70%> 
- Note A crash, next, ReplicaSetController check pod number is one, it is not equal desired number two. ReplicaSetController add the changing infomation to  ReplicaSetController's queue. 
<image src ="image/ReplicaSet2.jpg" width=70%> 
- ReplicaSet = 2, two App1s are on Note B
ReplicaSetController start multiple  Goroutines, the Goroutines  will get taks from the que. and then create new pod to match the desired number
<image src ="image/ReplicaSet3.jpg" width=70%> 

## When to use a ReplicaSet?
- ReplicaSet do not support update, expansion and shrinkage operation.
- Using Deployments instead of directly using ReplicaSets, unless you require custom update orchestration or don't require updates at all.




####################################################################
Today we leaned Kubernetes core concepts - ReplicaSet.
ReplicaSetController workflow
and use Deployments instead of directly using ReplicaSets


Thank you for watching, see you in the next class.


Figure 1. Pods overview 
Source:(https://d33wubrfki0l68.cloudfront.net/fe03f68d8ede9815184852ca2a4fd30325e5d15a/98064/docs/tutorials/kubernetes-basics/public/images/module_03_pods.svg)

