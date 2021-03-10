# ConfigMaps
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/cm-256.png?raw=true" width="50">  

## What is ConfigMap? 
- A ConfigMap is an API object used to store non-confidential data in key-value pairs. 
- A ConfigMap allows you to decouple environment-specific configuration from your container images, so that your applications are easily portable.
## How to use ConfigMap?
There are four  ways, I  can use a ConfigMap to configure a container inside a Pod:
- Inside a container command and args
- Environment variables for a container, Environment variables do not support change value on fly.
- Add a file in read-only volume, for the application to read, that way support change value on fly.
- Write code to run inside the Pod that uses the Kubernetes API to read a ConfigMap
  
### How to create a ConfigMap?
#### File style
I'll create a application.properties and mount to busybox image. The style support chnage value on fly
The yaml file has two parts, first part create a application.properties file. Second part, create a busybox pod and mount the application.properties file.

configmap-file.yaml
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: propertiesconfig
data:
  application.properties: | (Vertical line make config map as file)
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
            mountPath: "/config" - this is mount point, if the folder does not existing, K8S will create. 
          command: ["/bin/sh", "-ec", "sleep 1000"]  this is  continer start command, and keep  continer running
      volumes: next volumes define
        - name: config volume name is config , hte name match above volumeMounts name.
          configMap: the volume type is configMap
            name: propertiesconfig should be map to ConfigMap object name.
            items:
            - key: "application.properties" the key is ConfigMap object data: application.properties
              path: "application.properties"  mounted into the Pod at path /config. the full file path is /config/application.properties
# template end

```   
First create the three objects, configmap, deploymnets, pod
`kubectl apply -f configmap-file.yaml `  
Second, check ConfigMap object.
`kubectl get ConfigMap propertiesconfig -o yaml`  
next get pod name
`kubectl get pod`  
and then go into busy pod to check value of application.properties
`kubectl exec -it busybox-deployment-XXX -- sh `
Let's verify  configmap support changing on fly. 
First step, change eisxitng config map value
`kubectl edit configmap client-servic` 
Second step, go into busy pod to check new value of application.properties
`kubectl exec -it busybox-deployment-XXX -- sh ` 
Final Delete three objects
`kubectl delete -f configmap-file.yaml`  

Abovei try configmap with file style, let me demo how to use configmap as env parameters

The yaml file has two parts, first part create a  key-value config map  . Second part, create a busybox pod and inject the  key-value config map as env parameter. The style does not support chnage value on fly.
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
              name: envconfig must eque with ConfigMap name.

# template end

```

First create the three objects, configmap, deploymnets, pod
`kubectl apply -f configmap-env-variable.yaml `  
Second, check ConfigMap object.
`kubectl get ConfigMap envconfig -o yaml` 
next get pod name 
`kubectl get pod`
verify env parameters  
`kubectl exec -it busybox-deployment-XXX -- env `



####################################################################
Today we leaned Kubernetes core concepts - ConfigMap.
What is ConfigMap

Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume.

Create ConfigMap in two ways.


Thank you for watching, see you in the next class.


