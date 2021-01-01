# Secrets
Kubernetes Secrets let you store and manage sensitive information, such as passwords, OAuth tokens, and ssh keys. Storing confidential information in a Secret is safer and more flexible than putting it verbatim in a Pod definition or in a container image. See Secrets design document for more information.

A Secret is an object that contains a small amount of sensitive data such as a password, a token, or a key. Such information might otherwise be put in a Pod specification or in an image. Users can create Secrets and the system also creates some Secrets
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/secret-256.png?raw=true" width="100">
https://kubernetes.io/docs/concepts/configuration/secret/