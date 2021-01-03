# Service
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/svc-256.png?raw=true" width="50">   

## What is service?
- An abstract way to expose an application running on a set of Pods as a network service.
- ServiceTypes 
  - ClusterIP
  - NodePort
  - LoadBalancer
  - ExternalName
## Why need service?
- Service discovery without modify your application 
  -  Service - environment variables 
  -  DNS
- Access point of group of pods
- Load-balance across
  -  rr: round-robin(default)
  -  lc: least connection (smallest number of open connections)
  -  dh: destination hashing
  -  sh: source hashing
  -  sed: shortest expected delay
  -  nq: never queue
## How to create a Service?
```
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: MyApp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 9376
```


With Kubernetes you don't need to modify your application to use an unfamiliar service discovery mechanism. Kubernetes gives Pods their own IP addresses and a single DNS name for a set of Pods, and can load-balance across them.
https://kubernetes.io/docs/concepts/services-networking/service/

