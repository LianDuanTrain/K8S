Welcome to our class. Today we will learn Secrets.

## What is Secrets?
Kubernetes Secrets store and manage sensitive information.
- Passwords
- OAuth tokens
- SSH keys


### How to inject the configuration item of the application in K8S?
There are four different ways.
- Inside a container command and args
- Environment variables for a container
- Add a file in read-only volume, for the application to read
- Write code to run inside the Pod that uses the Kubernetes API to read a ConfigMap

## How to create Secrets?
### Comman Line
```
kubectl create secret generic command-secret \
  --from-literal=username=lian \
  --from-literal=password='123'
```
`kubectl get secret`  
`kubectl get secret command-secret -o yaml`   
```echo 'bGlhbg==' | base64 --decode```
### Key value pair
```
apiVersion: v1
kind: Secret
metadata:
  name: key-value-secret
type: Opaque 
data:
# echo  'lian' | base64
# echo  '123' | base64
  username: bGlhbgo=
  password: MTIzCg==
```
`kubectl get secret`  
`kubectl get secret key-value-secret -o yaml`

### File
apiVersion: v1
kind: Secret
metadata:
  name: file-secret
type: Opaque
# echo  'hello, I am file secret.' | base64
data:
  mysecret: |
   aGVsbG8sIEkgYW0gZmlsZSBzZWNyZXQuCg==

`kubectl get secret`  
`kubectl get secret file-secret -o yaml`

## How to inject Secrets in Pod?

```
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
          env:
            - name: SECRET_USERNAME
              valueFrom:
                secretKeyRef:
                  name: key-value-secret
                  key: username
            - name: SECRET_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: key-value-secret
                  key: password      
          volumeMounts: 
          - name: config
            readOnly: true
            mountPath: "/config"
          command: ["/bin/sh", "-ec", "sleep 1000"]  
      volumes:
        - name: config
          secret:
            secretName: file-secret
# template end
```
`kubectl get pod`  
`kubectl exec -it busybox-deployment-XXX -- sh `

####################################################################
Today we leaned Kubernetes core concepts - secret and create the secret in two ways..

Thank you for watching, see you in the next class.


