# Service
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/svc-256.png?raw=true" width="50">   

## What is service?
- An abstract way to expose an application running on a set of Pods as a network service.
- ServiceTypes 
  - ClusterIP
  - NodePort
  - LoadBalancer
  - ExternalName

## How to create a Service?
```
apiVersion: v1
kind: Service
metadata:
  name: springbootdemo
spec:
  selector:
    app: springbootdemo
  ports:
    - protocol: TCP
      port: 9999
      targetPort: 9999
```
- Access Service  
  - `kubectl get pods`    
  - `kubectl get endpoints` 
  - `kubectl logs springbootdemo-deployment-XXX`   
  - `kubectl port-forward service/springbootdemo 9999:9999`   
    - `curl 127.0.0.1:9999`  

## Why need service?
- Service discovery without modify application 
  -  Environment variables
     - `kubectl get pods`   
     - `kubectl exec -it springbootdemo-deployment-XXX -- env`  
  -  DNS
     - busybox
       - `kubectl run  -i --tty busybox --image=busybox:1.28.4 --restart=Never -- sh`
       - `nslookup springbootdemo`
     - K8S dnsutils
       - `kubectl apply -f https://k8s.io/examples/admin/dns/dnsutils.yaml`
       - `kubectl exec -i -t dnsutils -- nslookup kubernetes.default`
       - `kubectl exec -i -t dnsutils -- nslookup springbootdemo`
  
- Access point for group of pods

## Service Load-Balance Types
-  Userspace
-  Iptables proxy mode
-  IPVS proxy mode
-  Check Load-Balance Types
   - `kubectl get -n kube-system configmap kube-proxy -o yaml`
   - `minikube ssh`
     - `grep -e ipvs -e nf_conntrack_ipv4 /lib/modules/$(uname -r)/modules.builtin`  
     - `sudo iptables -t nat -L KUBE-SERVICES -n |grep springbootdemo`









