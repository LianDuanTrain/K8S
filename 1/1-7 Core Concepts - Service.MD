# Service
An abstract way to expose an application running on a set of Pods as a network service.
With Kubernetes you don't need to modify your application to use an unfamiliar service discovery mechanism. Kubernetes gives Pods their own IP addresses and a single DNS name for a set of Pods, and can load-balance across them.
https://kubernetes.io/docs/concepts/services-networking/service/

<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/svc-256.png?raw=true" width="100">