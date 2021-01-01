Welcome to our class. Today we learn Kubernetes Architecture
# Kubernetes Architecture
[<image src="https://d33wubrfki0l68.cloudfront.net/d35c2b375b43b4fa374ae834f95224975418e33f/6b47b/images/blog/2018-06-05-11-ways-not-to-get-hacked/kubernetes-control-plane.png" alert="Figure 1">] 


https://elastisys.com/wp-content/uploads/2018/01/kubernetes-ha-setup.pdf?x83281

K8s cluster has two type nodes, master node and worker node.

## Master
Master node has four components,apiserver,controller managers,scheduler etcd.

- apiserver: a REST API supporting basic CRUD operations on API objects (such as pods, deployments, and services).
This is the endpoint that a cluster administrator communicates , for example, using kubectl. The apiserver is stateless. Instead, it uses a distributed key-value storage system (etcd) as its backend for storing all cluster state.

- controller managers:
The Kubernetes controller manager is a daemon that embeds the core control loops shipped with Kubernetes. 

 In Kubernetes, a controller is a control loop that watches the shared state of the cluster through the apiserver and makes changes attempting to move the current state towards the desired state. 

Examples of controllers that ship with Kubernetes today are the replication controller, endpoints controller, namespace controller, and service accounts controller.


- scheduler: 
Takes care of pod placement across the set of available nodes,  balance resource consumption to not place overload on any cluster node.

- Etcd:
Etcd is a consistent and highly-available key value store used as Kubernetes' backing store for all cluster data.
Make sure you have a back up plan for those data.

## Nodes
The node components run on every cluster node. 
- Container runtime: 
  such as Docker Contained , to execute containers on the node.
- kubelet: 
  executes containers (pods) on the node as dictated by the scheduler, and ensures the health of those pods (for example, by restarting failed pods).

- kube-proxy:

a network proxy/load balancer that implements the Service abstraction.
It programs the iptables rules on the node to redirect service IP requests to one of its registered backend pods.


Figure 1. kubernetes-control-plane.png
Source:(https://kubernetes.io/blog/2018/07/18/11-ways-not-to-get-hacked/)


####################################################################
Today we leaned Kubernetes Architecturs. Kubernetes has two type nodes, master and worker.
Master node has apiserver,controller managers,scheduler, etcd.
Worker node include Container runtime, kubelet, and kube-proxy.

Thank you for watching, see you in the next class.