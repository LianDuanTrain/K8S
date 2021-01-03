# Secrets
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/secret-256.png?raw=true" width="50">  

## What is Secrets?
Kubernetes Secrets let you store and manage sensitive information.
- Passwords
- OAuth tokens
- SSH keys

## How to create Secrets?
```
kubectl create secret generic dev-db-secret \
  --from-literal=username=devuser \
  --from-literal=password='S!B\*d$zDsb='
```
```
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
type: Opaque
data:
  username: YWRtaW4=
  password: MWYyZDFlMmU2N2Rm
```


https://kubernetes.io/docs/concepts/configuration/secret/