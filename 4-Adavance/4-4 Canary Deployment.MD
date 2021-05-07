
# Canary Deployment
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/ing-256.png?raw=true" width="50"> 

## Topics
- What is Canary Deployment?
- How to implement Canary Deployment with Ingress?
- Demo  

# What is Canary Deployment?

- App v1    
<image src="Canary Deployment0.png" width="70%"/>  
- App v1 and App v2   
<image src="Canary Deployment.png" width="70%"/>  

- A canary deployment
- Roll out new code to a subset of users as an initial test.  
# How to implement Canary Deployment with Nginx Ingress?
- Customization Ingress Resource
  - enable Ingress addons
  - enable canary in Ingress Resource
- Canary Type
  - header
  - cookie
  - weight
  - Canary rules are evaluated in order of precedence
   - canary-by-header -> canary-by-cookie -> canary-weight
# Demo 
## APPs
### V1 
- Deployment
  - springbootdemo-deployment-v1
- Pod   
  - springbootdemo-v1 
- Service
  - springbootdemo-service-v1
### V2 
- Deployment
  - springbootdemo-deployment-v2
- Pod   
  - springbootdemo-v2  
- Service
  - springbootdemo-service-v2 
### Ingress
- www.springbootdemo.com - > springbootdemo-service-v1 
## Weight Ingress
nginx.ingress.kubernetes.io/canary: "true"
nginx.ingress.kubernetes.io/canary-weight: "50"
## Weight Ingress
nginx.ingress.kubernetes.io/canary: "true"
nginx.ingress.kubernetes.io/canary-by-header: "Region"
nginx.ingress.kubernetes.io/canary-by-header-pattern: "VA|MD"