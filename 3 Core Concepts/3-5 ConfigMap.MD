

# ConfigMaps
  <image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/cm-256.png?raw=true" width="50"/>

## Topics         
- What is ConfigMap? 
- How to use ConfigMap?
- How to create a ConfigMap?

### What is ConfigMap? 
- An API object used to store non-confidential data in key-value pairs. 
- Decouple environment-specific configuration from container images.
### How to use ConfigMap?
There are four different ways.
- Inside a container command and args
- Environment variables for a container
- Add a file in read-only volume, for the application to read
- Write code to run inside the Pod that uses the Kubernetes API to read a ConfigMap

### How to create a ConfigMap?
#### File 
configmap-file.yaml
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: propertiesconfig
data:
  application.properties: |
    bean.message=Testing reload

---
# API Version  
apiVersion: apps/v1
kind: Deployment
# Deployment metadata start
metadata:
  name: busybox-deployment
  labels:
    app: busybox
# Deployment metadata end
# Pod spec start    
spec:
  replicas: 1
  selector:
    matchLabels:
      app: busybox
# Pod spec end       
# template start      
  template:
    metadata:
      labels:
        app: busybox
    spec:
      containers:  
        - name: busybox
          image: busybox       
          volumeMounts: 
          - name: config
            mountPath: "/config"
          command: ["/bin/sh", "-ec", "sleep 1000"]  
      volumes:
        - name: config
          configMap:
            name: propertiesconfig
            items:
            - key: "application.properties"
              path: "application.properties"
# template end

```   

`kubectl apply -f configmap-file.yaml `  
`kubectl get ConfigMap propertiesconfig -o yaml`  
`kubectl get pod`  
`kubectl exec -it busybox-deployment-XXX -- sh `
`kubectl edit configmap client-servic` 
`kubectl exec -it busybox-deployment-XXX -- sh ` 
`kubectl delete -f configmap-file.yaml`  


#### ENV
configmap-env-variable.yaml
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: envconfig
data:
  loglevel: debug 

---
# API Version  
apiVersion: apps/v1
kind: Deployment
# Deployment metadata start
metadata:
  name: busybox-deployment
  labels:
    app: busybox
# Deployment metadata end
# Pod spec start    
spec:
  replicas: 1
  selector:
    matchLabels:
      app: busybox
# Pod spec end       
# template start      
  template:
    metadata:
      labels:
        app: busybox
    spec:
      containers:  
        - name: busybox
          image: busybox       
          command: ["/bin/sh", "-ec", "sleep 1000"] 
          envFrom:
          - configMapRef:
              name: envconfig

# template end

```


`kubectl apply -f configmap-env-variable.yaml `  
`kubectl get ConfigMap envconfig -o yaml`  
`kubectl get pod`  
`kubectl exec -it busybox-deployment-XXX -- env `




