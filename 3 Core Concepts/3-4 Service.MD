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
- Service discovery without modify application 
  -  Environment variables 
  -  DNS
- Access point for group of pods

## How to create a Service?
```
apiVersion: v1
kind: Service
metadata:
  name: springbootdemo
spec:
  selector:
    app: springbootdemo
  ports:
    - protocol: TCP
      port: 9999
      targetPort: 9999
```
### Access Service  
`kubectl get pods`  
`kubectl  logs springbootdemo-deployment-94658b785-4xjsd`   
`kubectl port-forward service/springbootdemo 9999:9999`   
`curl 127.0.0.1:9999`  


