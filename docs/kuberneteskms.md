## Secrets Management for Azure Kubernetes Service (AKS)
### Context
Every infrastructure, service or application deployment involves working with, configuring and managing secrets, passwords, encryption keys that help secure the platform and the application in question. Here are the primary  A Kubernetes deployment on Azure using Azure Container Service (AKS) enncompasses the following broad areas which could utilize a Key Management System for managing associated secrets for the deployment.

### Current

#### etcd Key/Value Encryption
Kubernetes utilizes etcd to store and share configuration data bwtween various internal services on the Master. etcd stores its data in plain text, if someone is able to connect to the etcd store, all configuration parameters, kubernetes confiuration secrets and API tokens of the kubernetes cluster are made available to the connecting user.

The kubernetes-kms grpc [server] (https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/) sits on all masters and facilitates communication between Azure Key Vault, by creating a key vault and an encryption key and providing this encryption key as an configuration to the kubernetes data encryption at rest feature. A flag needs to be set in the ACS Engine configuration to enable this feature.

#### etcd Database Encryption at Rest

Kubernetes utilizes etcd to store and share config data bwtween various internal services on the Master. etcd stores its data in plain text, if someone is able to connect to the etcd store, all configuration parameters, kubernetes confiuration secrets and API tokens of the kubernetes cluster are made available to the connecting user.


###Future 

#### Cluster Communication

Cluster communication is not encrypted by default and Azure KMS intergation is currently not implemented.

#### Node Credentials

##### Linux

SSH Key and Username for the cluster - Azure KMS intergation is currently not implemented

##### Windows

Username & Password for Windows Cluster - Azure KMS intergation is currently not implemented

#### Kubelet

The Kubelet is TLS enabled and uses a Certificate/Key Pair - Azure KMS intergation is currently not implemented

#### Pod Security Policies

#### Kube Config

Secrets on Kubeconfig - Azure KMS intergation is currently not implemented

#### Master Secrets

Masters have a Private Key - Azure KMS intergation is currently not implemented

#### Application Secrets

Can utilize Azure Key vault, Hashicorp Key Vault
