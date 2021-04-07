# Ingress 
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/ing-256.png?raw=true" width="50">  

## Topics         
- Get Nginx Ingress Configuration Detail
- Add Nginx Ingress Annotations

### Get Nginx Ingress Configuration Detail
Add these Kubernetes annotations to specific Ingress objects to customize their behavior.
- Check Nginx config 
  - `kubectl describe ingress ingress-demo --namespace=k8s-training`  
  - `kubectl get pods --namespace=kube-system`
  - `kubectl exec -it ingress-nginx-controller-XXX -- sh -ls`  

- Scale Pod
  - `kubectl scale deployment/springbootdemo-deployment --replicas=2 --record=true --namespace=k8s-training`
  - `kubectl get pods --namespace=k8s-training` 
  - `kubectl describe ingress ingress-demo --namespace=k8s-training`

### Add Nginx Ingress Annotations  
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
  
