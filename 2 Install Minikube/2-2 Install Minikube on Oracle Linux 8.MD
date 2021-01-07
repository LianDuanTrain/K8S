# Install Minikube on Oracle Linux 8 

### Download Minikube
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-latest.x86_64.rpm   
sudo rpm -ivh minikube-latest.x86_64.rpm
```
### Start Minikube
`minikube start`  
### Check Minikube Status  
`minikube status` 
## Install  kubectl and check
`minikube kubectl -- get po -A`  
`kubectl version`    
`sudo ln -s $(which minikube) /usr/local/bin/kubectl` 


