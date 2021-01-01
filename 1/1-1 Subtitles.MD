Welcome to our class. Today we will Overview Kubernetes
https://www.xenonstack.com/insights/kubernetes-deployment/
## What is Kubernetes?  

Kubernetes (also known as k8s or "kube") is an open source container orchestration platform.
Kubernetes is able to  automates  deploying, managing, and scaling containerized applications.

Kubernetes was originally developed and designed by engineers at Google. Google was one of the early contributors to Linux container technology.

Google generates more than 2 billion container deployments a week, all powered by its internal platform, Borg. 
Borg was the predecessor to Kubernetes, and the lessons learned from developing Borg over the years became the primary influence behind much of Kubernetes technology.


## Why you need Kubernetes?
[<image src="https://d33wubrfki0l68.cloudfront.net/26a177ede4d7b032362289c6fccd448fc4a91174/eb693/images/docs/container_evolution.svg">] 


Why you need Kubernetes？there are three-generation types for deployment application.

The first traditional deployment, deploy the application on top of the operation system. all the depends Libraries have to directly operating system.

In the second virtualized deployment, Use a Virtual Machine to deploy applications.  one physical box has multiple virtual machines.  each virtual machine has an isolated operation system, the application depends on the library and application.
The virtual machine support a backup snapshot and easy to restore to the previous snapshot.

Thrid, container deployment, Install container runtime support in the physical machine.
create a docker image or image compatible with the CRI(Container Runtime Interface).
the image includes the operating system,  APP depends on the library, APPc onfigration and application. containers start based on  image, Image is a blueprint for the container 


What is the difference between the container and VM?
	
The VM is a virtual machine, virtualize enter the operating system on your physical box so the more memory, hard disk, CPU resource then Docker.
Container is ruining the top of the contained runtime so container needs the memory, CPU, hard disk, resourceless than the virtual machine.
contained APP easy to distributed to QA and the production ENV.

There are main founction of k8s.
- Service discovery and load balancing， internal discovery through DNS, and service used to load balancing purpose. 
- Storage orchestration. K8s support supports multiple storages via plungin, such as local, nfs, , public cloud fast storage, etc.
- Automated rollouts and rollbacks. by matching the current state to the target state, rollback when the update fails.
- Automatic bin packing. you can set the required (requests) resources and limit resources (limits) for pod scheduling
- Self-healing, Built-in health check strategy, automatically discover and handle error in the cluster,  replace pod nodes that need to be restarted
- Secret and configuration management,  Key and configuration management. For sensitive information such as passwords, the account is stored in secret, and the configuration file of the application is stored in configmap to avoid package  the configuration file in the image and increase the flexibility of container layout
- Batch execution, through job and cronjob to provide of single batch tasks and cyclic scheduled tasks.

####################################################################
Today we Overview Kubernetes. And know What is Kubernetes?  and Why you need Kubernetes?

Thank you for watching, see you in the next class.


https://cloud.tencent.com/developer/article/1474698

