# ReplicaSet

<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/rs-256.png?raw=true" width="50">  

## What is ReplicaSet?
- A ReplicaSet purpose is creating and deleting Pods as needed to reach the desired number. 
- When a ReplicaSet needs to create new Pods, it uses its Pod template.


## How a ReplicaSet works?

- ReplicaSet = 2, one App1 is on Note A and one App1 is on Note B
<image src ="image/ReplicaSet1.jpg" width=70%> 
- Note A crash  
<image src ="image/ReplicaSet2.jpg" width=70%>   
- ReplicaSet = 2, two App1s are on Note B  
<image src ="image/ReplicaSet3.jpg" width=70%> 

## When  using  a ReplicaSet?
- ReplicaSet do not support update, expansion and shrinkage operation.
- Using Deployments instead of directly using ReplicaSets, unless you require custom update orchestration or don't require updates at all.

https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/
