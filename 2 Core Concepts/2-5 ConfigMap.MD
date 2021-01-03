# ConfigMaps
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/cm-256.png?raw=true" width="50">  

## What is ConfigMap? 
- An API object used to store non-confidential data in key-value pairs. 
- Decouple environment-specific configuration from container images.
## How to use ConfigMap?
There are four different ways that can use a ConfigMap to configure a container inside a Pod:
- Inside a container command and args
- Environment variables for a container
- Add a file in read-only volume, for the application to read
- Write code to run inside the Pod that uses the Kubernetes API to read a ConfigMap

## How to create a ConfigMap?
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: game-demo
data:
  # property-like keys; each key maps to a simple value
  player_initial_lives: "3"
  ui_properties_file_name: "user-interface.properties"

```   
`kubectl create configmap special-config --from-literal=special.how=very --from-literal=special.type=charm`


https://kubernetes.io/docs/concepts/configuration/configmap/

