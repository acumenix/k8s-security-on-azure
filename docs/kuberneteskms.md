## Secrets Management for Azure Kubernetes Service (AKS)
### Context
Every infrastructure, service or application deployment involves working with, configuring and managing secrets, passwords, encryption keys that help secure the platform and the application in question.In the following article. A Kubernetes deployment on Azure using Azure Container Service (AKS)


#### etcd cluster communication
etcd stores its data in plain text, if someone is able to connect to the etcd store, all configuration parameters, kubernetes confiuration secrets and API tokens of the kubernetes cluster are made available to the connecting user.

the hexadite grpc servers sits on all masters and facilitates communication between Azure Key Vault, by creating a key vault and an encryption key and providing this envryption key as an configuration to the kubernetes data encryption at rest feature (https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/)

#### Cluster Communication

#### Node Credentials

##### Linux


##### Windows

#### Kubelet

#### Pod Security Policies

#### Kube Config

#### Master Secrets

#### Application Secrets