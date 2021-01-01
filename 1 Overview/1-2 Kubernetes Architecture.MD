# Kubernetes Architecture
[<image src="https://d33wubrfki0l68.cloudfront.net/d35c2b375b43b4fa374ae834f95224975418e33f/6b47b/images/blog/2018-06-05-11-ways-not-to-get-hacked/kubernetes-control-plane.png" name="Figure 1">] 


## Master
The master components.  
- Apiserver
- Controller managers
- Scheduler
- Etcd

## Nodes
The node components run on every cluster node. 
- Container Runtime
- Kubelet
- Kube-proxy


Figure 1. kubernetes-control-plane.png
Source:(https://kubernetes.io/blog/2018/07/18/11-ways-not-to-get-hacked/)