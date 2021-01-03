Welcome to our class. Today we will learn 

# Service
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/svc-256.png?raw=true" width="50">   

## What is service?
- Service access point of a group of Pods.  
- ServiceTypes 
  - ClusterIP is default service type. and it is internal IP for cluster. Can not access outside.
  - NodePort, export port of Node. I can access my app from outside. It usually for debugging app in dev env. the port range is from 30000-32767. 
  - LoadBalancer, your clould  service will provider LoadBalancer.
  - ExternalName, expose server via DNS name.
  
## Why need service?
- K8s provide Service discovery function without modify application. The server  registry doe not need. The servers are able to access eacth other via service name. There are two ways.  
  -  environment variables 
  -  DNS
- Pods are nonpermanent resources. Each Pod gets its own IP address so need a access point for group of pods.
- service implemant Load-balance across, the typs are below:
  -  rr: round-robin(default)
  -  lc: least connection (smallest number of open connections)
  -  dh: destination hashing - smallest number of open connections
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


Thank you for watching, see you in the next class.


Figure 1. Pods overview 
Source:(https://d33wubrfki0l68.cloudfront.net/fe03f68d8ede9815184852ca2a4fd30325e5d15a/98064/docs/tutorials/kubernetes-basics/public/images/module_03_pods.svg)

