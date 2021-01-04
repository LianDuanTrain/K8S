Welcome to our class. Today we will learn 

# ConfigMaps
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/cm-256.png?raw=true" width="50">  

## What is ConfigMap? 
- A ConfigMap is an API object used to store non-confidential data in key-value pairs. 
- A ConfigMap allows you to decouple environment-specific configuration from your container images, so that your applications are easily portable.
## How to use ConfigMap?
There are for  ways, I  can use a ConfigMap to configure a container inside a Pod:
- Inside a container command and args
- Environment variables for a container, Environment variables do not support change value on fly.
- Add a file in read-only volume, for the application to read, that way support change value on fly.
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

####################################################################
Today we leaned Kubernetes core concepts - ConfigMap.
What is ConfigMap

Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume.

Create ConfigMap in two ways.


Thank you for watching, see you in the next class.


