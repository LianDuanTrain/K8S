# Ingress Advice
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/ing-256.png?raw=true" width="50">  

## Topics         
- How to get Minikube Nginx Ingress Controller Configuration Detail?
- Add Nginx Ingress Controller Customization Parameter
- How to get Nginx Ingress Object configuration detail?
- Add Nginx Ingress Object Customization Parameter

### How to get Minikube Nginx Ingress Controller Configuration Detail?
- Check Minikube version   
  - `minikube version` 
- Retrieve Current Nginx Ingress Controller Configuration
  - `kubectl config set-context --current --namespace=kube-system`   
  - `kubectl get pods`  
  - `kubectl describe pods ingress-nginx-controller-XXX-s5m2k`   
  - `kubectl exec -it ingress-nginx-controller-XXX -- sh -ls` 

### Add Nginx Ingress Controller Customization Parameter
- Get ConfigMap name on Git 
  - https://github.com/kubernetes/minikube/tree/v1.18.0
  - List of Parameter
    -https://github.com/kubernetes/ingress-nginx/blob/master/docs/user-guide/nginx-configuration/configmap.md
- Edit  
  - `kubectl edit cm -n kube-system nginx-load-balancer-conf`  
- Check  
  - `kubectl logs ingress-nginx-controller-XXX`   
  - `kubectl exec -it ingress-nginx-controller-XXX -- sh -ls`   

### How to get Nginx Ingress Object configuration Detail?
- `kubectl describe ingress ingress-demo --namespace=k8s-training` 
- Scale Pod  
  - `kubectl scale deployment/springbootdemo-deployment --replicas=2 --record=true --namespace=k8s-training`
  - `kubectl get pods --namespace=k8s-training` 
  - `kubectl describe ingress ingress-demo --namespace=k8s-training`



### Add Nginx Ingress Object Customization Parameter
Add these Kubernetes annotations to specific Ingress objects to customize their behavior.  
https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations     
```  annotations:
    kubernets.io/ingress.class: nginx
    nginx.ingress.kubernetes.io/proxy-read-timeout: "3600"
    nginx.ingress.kubernetes.io/proxy-send-timeout: "3600"
    nginx.ingress.kubernetes.io/load-balance : "ewma"
```    
- `kubectl apply -f https://raw.githubusercontent.com/LianDuanTrain/K8S/main/4-Adavance/ingress-demo-v2.yaml` 
- `kubectl describe ingress ingress-demo --namespace=k8s-training`
- `kubectl logs ingress-nginx-controller-XXX -n` 
  
- Test springbootdemo
  - curl springbootdemo.com
  - curl springbootdemo.com/sys|jq
  
