# Rolling Update Deployment
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/deploy-256.png?raw=true" width="50">  

## Topics
- What is Deployment?
- How to Rolling Update with Deployment?
- Demo  

# What is Deployment?
A Deployment provides declarative updates for Pods and ReplicaSets.

```
|---Deployment   
    |   
    |---ReplicaSets   
        |   
        |--- Pods 
```          

# How to Rolling Update with Deployment?
Rolling updates allow Deployments' update to take place with zero downtime by incrementally updating Pods instances with new ones. 

## Type 
- Update Image
    - `kubectl -n k8s-training set image deploymentsName containersName=image  --record=true`
- Apply Update YAML File
    - `kubectl apply -f rolling-update-demo-v2.yaml  --record=true`
    - Strategy
        - Recreate
        - RollingUpdate (default value)
            - Max Unavailable : .spec.strategy.rollingUpdate.maxUnavailable
            - Max Surge : .spec.strategy.rollingUpdate.maxSurge
            - Progress Deadline Seconds : .spec.progressDeadlineSeconds
            - Min Ready Seconds : .spec.minReadySeconds
            - Revision History Limit : .spec.revisionHistoryLimit  


# Demo 
- `minikube addons enable ingress`  
- `minikube ip`  
- ```
  sudo sh -c "echo '$(minikube ip) www.springbootdemo.com' >> /etc/hosts"
  cat   /etc/hosts
  ```  
- `kubectl apply -f rolling-update-demo-v1.yaml  --record=true` 
- `kubectl get deployments -n k8s-training  rolling-update-deployment`  
- `kubectl get pods -n k8s-training`
- `kubectl describe pods -n k8s-training rolling-update-deployment-b956d5c99-2qntp`
- `kubectl get rs -w -n k8s-training`
- `curl www.springbootdemo.com`  
## Demo Update Image
- `kubectl -n k8s-training set image deployments/rolling-update-deployment springbootdemo=lianduantraining/springbootdemo:v2  --record=true`
### Rollout Status   
- `kubectl -n k8s-training rollout status deployment/rolling-update-deployment`
- `kubectl -n k8s-training rollout pause deployment/rolling-update-deployment`
- `kubectl -n k8s-training rollout resume deployment/rolling-update-deployment`
### Describe Deployment
- `kubectl -n k8s-training describe deployment rolling-update-deployment`
### Rollout History
- `kubectl -n k8s-training rollout history deployment rolling-update-deployment`
### Check APP Version
- `curl www.springbootdemo.com` 
### Clean Up
- `kubectl delete -f rolling-update-demo-v1.yaml` 

## Demo Apply Update YAML File
- `kubectl apply -f rolling-update-demo-v2.yaml  --record=true` 
 - ```
   strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 2
      maxUnavailable: 2
    minReadySeconds: 15
   ```   

### Check Rollout Status   
- `kubectl -n k8s-training rollout status deployment/rolling-update-deployment` 
- `kubectl -n k8s-training rollout pause deployment/rolling-update-deployment`  
- `kubectl -n k8s-training rollout resume deployment/rolling-update-deployment`   
### Describe Deployment
- `kubectl -n k8s-training describe deployment rolling-update-deployment`
### Rollout History
- `kubectl -n k8s-training rollout history deployment rolling-update-deployment`  

### Check Rollout APP Version
- `curl www.springbootdemo.com`

### Check RS
- `kubectl get rs -w -n k8s-training`
### Undo Rollout
  - `kubectl -n k8s-training rollout undo deployment/rolling-update-deployment --to-revision=1`  

### Check Undo Rollout APP Version
- `curl www.springbootdemo.com`   









