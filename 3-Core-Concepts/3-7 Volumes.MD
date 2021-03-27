# Volumes
<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/vol-256.png?raw=true" width="50">

## What is Volumes?
Volume is a shared directory in a pod that can be accessed by multiple containers
- The volume is defined on the pod, and then mounted by multiple containers of a pod to a specific file directory
- The life cycle of volume and pod in Kubernetes is the same, but not related to the life cycle of the container


## Which types of Volumes?
- emptyDir
- hostPath
- secret
- configMap
- gitRepo
- glusterfs
- awsElasticBlockStore
- gcePersistentDisk
- azureDisk & azureFile


