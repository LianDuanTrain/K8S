Welcome to our class. Today we will learn Secrets.

## What is Secrets?
Kubernetes Secrets store and manage sensitive information.
- Passwords
- OAuth tokens
- SSH keys

## I can create Secrets in two ways
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

####################################################################
Today we leaned Kubernetes core concepts - secret and create the secret in two ways..

Thank you for watching, see you in the next class.


