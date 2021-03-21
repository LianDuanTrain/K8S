Welcome to our class. Today we will learn Secrets.

## Topics         
- What is Secrets? 
- How to create Secrets?
- How to inject the Secrets item of the application in K8S?

### What is Secrets?
Kubernetes Secrets store and manage sensitive information. There are three types of secrets,
- Passwords
- OAuth tokens
- SSH keys
Today, my demos are  password type.


The Secrets is stored in etcd in k8s, while the Secrets is only base 64 edcoding in etcd. If any one able to access K8s etcd, the guy can access and read the Secrets. Us K8s Secrets need review woth your secuiorty team because the it is not realy Secre.

Next Topic 
### How to create Secrets?
Secrets are created by three ways, Command Line, Key-value pair in API defnation file. Filetype in  API defnation file

#### Command Line
input value  will be auto encode with base64 in  Command Line
First step create secret from command-line from-literal is key word
```
kubectl create secret generic command-line-secret \
  --from-literal=username=lian \
  --from-literal=password='123'
```
Next step, check existing secret
`kubectl get secret command-line-secret -o yaml`      
Decode value  
```echo 'bGlhbg==' | base64 --decode``` 

`kubectl get secret`  there is only two  secrets, let me get all k8s name space. and try to get more secrets
`kubectl get namespace`  
`kubectl get secret -n kube-system`   

And then I demo create key value paare in yaml file
#### Key-value pair
```
apiVersion: v1
kind: Secret
metadata:
  name: key-value-secret is Secret name
type: Opaque 
data: includ key value paare, the value must be base64 encoding
# echo  'lian' | base64
# echo  '123' | base64
  username: bGlhbgo=
  password: MTIzCg==
```
`kubectl get secret`  
`kubectl get secret key-value-secret -o yaml`

next demo is , create a secret as file style
#### File
```
apiVersion: v1
kind: Secret
metadata:
  name: file-secret
type: Opaque
# echo  'hello, I am file secret.' | base64
data: mysecret is file name, pipe
  mysecret: | 
   aGVsbG8sIEkgYW0gZmlsZSBzZWNyZXQuCg==
```
`kubectl get secret`  
`kubectl get secret file-secret -o yaml`
The latest topic 
### How to inject the Secrets item of the application in K8S?
There are four different ways.
- Inside a container command and args
- Environment variables for a container
- Add a file in read-only volume, for the application to read
- Write code to run inside the Pod that uses the Kubernetes API to read a ConfigMap

Let me demo.
go thougth yaml file
#### Demo

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
          env: add env parameter from key-value-secret
            - name: SECRET_USERNAME env name 
              valueFrom:
                secretKeyRef:
                  name: key-value-secret is secret name
                  key: username
            - name: SECRET_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: key-value-secret
                  key: password   
          volumeMounts part for file secret mount
          volumeMounts: 
          - name: secret-config
            readOnly: true
            mountPath: "/secret-config", busy image does not have the folder, k8s will create when the conter start up.
          command: ["/bin/sh", "-ec", "sleep 1000"]  
      volumes:
        - name: secret-config
          secret:
            secretName: file-secret is secret name
# template end
```
`kubectl get pod`  
`kubectl exec -it busybox-deployment-XXX -- sh `

####################################################################
Today we leaned Kubernetes core concepts - secret 

- What is Secrets? 
  - Kubernetes Secrets store and manage sensitive **information**
- Demo Three ways to create Secrets?
- Inject the Secrets item to container.

Thank you for watching, see you in the next class.


