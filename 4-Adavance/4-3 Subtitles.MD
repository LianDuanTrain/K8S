# Blue/Green Deployment
## Topics
- What is Blue/Green Deployment?
- Demo  
  - Create Blue Deployment and Ingress
  - Create Green Deployment and Ingress
  - Switch network traffic from Blue to Green

## What is Blue/Green Deployment?
- A Blue/Green deployment is a way of accomplishing a zero-downtime upgrade to an - existing application. 
- The “Blue” version is the currently running copy of the application T
he “Green” version is the new version. 
- Once the green version is ready, traffic is rerouted to the new version.

Kubernetes has a really awesome built-in feature called Deployments. Deployments come with the ability to do rolling updates of containers when you update your application to a new version. Rolling updates are a great way to update applications because your app uses about the same amount of resources during an update as it does when not updating, all with minimal impact to performance and availability.

However, there are many legacy applications out there that don't work well with rolling updates. Some applications simply need to deploy a new version and cut over to it right away. For this, we need to perform a blue/green deployment. With blue/green deployments a new copy of the application (green) is deployed alongside the existing version (blue). Then the ingress/router to the app is updated to switch to the new version (green). You then need to wait for the old (blue) version to finish the requests sent to it, but for the most part traffic to the app changes to the new version all at once.



## What is Blue/Green Deployment?
- A Blue/Green deployment is a way of accomplishing a zero-downtime upgrade to an - existing application. 
- The “Blue” version is the currently running copy of the application T
he “Green” version is the new version. 
- Once the green version is ready, traffic is rerouted to the new version.


## Demo  
<image src ="greenblue.gif" width="70%">  

### Create a Blue Deployment
#### www.springbootdemo.com => springbootdemo-v1 service  
- `minikube addons enable ingress`  
- `minikube ip`  
- ```
  sudo sh -c "echo '$(minikube ip) www.springbootdemo.com' >> /etc/hosts"
  cat   /etc/hosts
  ```
- Deployment 
  - metadata => version: v1
- Pod   
  - metadata => version: v1
- Service
  - selector => version: v1

- `kubectl apply -f https://github.com/LianDuanTrain/K8S/blob/main/4-Adavance/Blue%20Green%20Deployment%20Yaml/springboot-demo-service-blue-v1.yaml`  

#### Test Service
  - `kubectl run  -it busybox --rm --image=yauritux/busybox-curl --restart=Never -n k8s-training -- sh -ls` 
  - `curl www.springbootdemo-v1`

### Create a Blue Ingress
  - service => name: springbootdemo-v1  
  - `kubectl apply -f https://github.com/LianDuanTrain/K8S/blob/main/4-Adavance/Blue%20Green%20Deployment%20Yaml/blue-ingress-demo.yaml`    
#### Test Blue Ingress
  - curl www.springbootdemo.com
  - curl www.springbootdemo.com/sys|jq

### Create a Green Deployment
#### test.springbootdemo.com => springbootdemo-v2 service   
- `minikube ip`  
- ```
  sudo sh -c "echo '$(minikube ip) test.springbootdemo.com' >> /etc/hosts"
  cat   /etc/hosts
  ```
- Deployment 
  - metadata => version: v2
- Pod   
  - metadata => version: v2
- Service
  - selector => version: v2

  
- `kubectl apply -f https://github.com/LianDuanTrain/K8S/blob/main/4-Adavance/Blue%20Green%20Deployment%20Yaml/springboot-demo-service-blue-v1.yaml`  

#### Test Service
  - `kubectl run  -it busybox --rm --image=yauritux/busybox-curl --restart=Never -n k8s-training -- sh -ls` 
  - `curl test.springbootdemo-v2`

### Create a Green Ingress
  - service => name: springbootdemo-v2
  - `kubectl apply -f https://github.com/LianDuanTrain/K8S/blob/main/4-Adavance/Blue%20Green%20Deployment%20Yaml/green-ingress-demo.yaml`   
#### Test Green Ingress
  - curl test.springbootdemo.com
  - curl test.springbootdemo.com/sys|jq  
  
### Switch Network Traffic from Blue to Green

- `kubectl patch ing/blue-ingress-demo --type=json -p='[{"op": "replace", "path": "/spec/rules/0/http/paths/0/backend/serviceName", "value":"springbootdemo-v2"}]' -n k8s-training` 
- `kubectl delete ingress blue-ingress-demo -n k8s-training`     




https://www.ianlewis.org/en/bluegreen-deployments-kubernetes

https://cloud.tencent.com/developer/article/1638413
https://juejin.cn/post/6844903927318577159

https://www.haproxy.com/blog/rolling-updates-and-blue-green-deployments-with-kubernetes-and-haproxy/


https://semaphoreci.com/blog/continuous-blue-green-deployments-with-kubernetes


https://blog.csdn.net/ljx1528/article/details/108801579

https://blog.csdn.net/shenshouer/article/details/49156299?utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control&dist_request_id=1331978.15078.16186674624086545&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control


https://www.youtube.com/watch?v=xUJbTnN3Dmw


https://martinfowler.com/bliki/BlueGreenDeployment.html


kubectl patch node k8s-node-1 -p '{"spec":{"unschedulable":true}}'


https://www.ianlewis.org/en/bluegreen-deployments-kubernetes