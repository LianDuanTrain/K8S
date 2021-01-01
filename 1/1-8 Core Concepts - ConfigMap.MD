# ConfigMaps
A ConfigMap is an API object used to store non-confidential data in key-value pairs. Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume.

A ConfigMap allows you to decouple environment-specific configuration from your container images, so that your applications are easily portable.

https://kubernetes.io/docs/concepts/configuration/configmap/

<image src ="https://github.com/kubernetes/community/blob/master/icons/png/resources/labeled/cm-256.png?raw=true" width="100">