## Build chain & content trust
### Context
Center for Internet Security (CIS) publishes a '[Security Kubernetes](https://www.cisecurity.org/benchmark/kubernetes/)' hardening guide, on which two benchmarks are based:
* [aquasecurity/kube-bench](https://github.com/aquasecurity/kube-bench)
* [docker/docker-bench-security](https://github.com/docker/docker-bench-security) (implemented as a daemonset for Kubernetes at [boeboe/docker-bench-security-kubernetes](https://github.com/boeboe/docker-bench-security-kubernetes))

These are good references for remediating lax security configurations that may come by default from kubernetes or acs-engine.

### Current State
These runs were produced on kubernetes 1.10 deployed via acs-engine 0.16.0 with the docker engine manually replaced with Docker CE 18.03 after provisioning.

#### CIS Kube-Bench
##### master
```
No CIS spec for 1.10 - using tests from CIS 1.2.0 spec for Kubernetes 1.8

[INFO] 1 Master Node Security Configuration
[INFO] 1.1 API Server
[PASS] 1.1.1 Ensure that the --anonymous-auth argument is set to false (Scored)
[PASS] 1.1.2 Ensure that the --basic-auth-file argument is not set (Scored)
[PASS] 1.1.3 Ensure that the --insecure-allow-any-token argument is not set (Scored)
[PASS] 1.1.4 Ensure that the --kubelet-https argument is set to true (Scored)
[PASS] 1.1.5 Ensure that the --insecure-bind-address argument is not set (Scored)
[FAIL] 1.1.6 Ensure that the --insecure-port argument is set to 0 (Scored)
[PASS] 1.1.7 Ensure that the --secure-port argument is not set to 0 (Scored)
[PASS] 1.1.8 Ensure that the --profiling argument is set to false (Scored)
[PASS] 1.1.9 Ensure that the --repair-malformed-updates argument is set to false (Scored)
[PASS] 1.1.10 Ensure that the admission control policy is not set to AlwaysAdmit (Scored)
[PASS] 1.1.11 Ensure that the admission control policy is set to AlwaysPullImages (Scored)
[PASS] 1.1.12 Ensure that the admission control policy is set to DenyEscalatingExec (Scored)
[FAIL] 1.1.13 Ensure that the admission control policy is set to SecurityContextDeny (Scored)
[PASS] 1.1.14 Ensure that the admission control policy is set to NamespaceLifecycle (Scored)
[PASS] 1.1.15 Ensure that the --audit-log-path argument is set as appropriate (Scored)
[PASS] 1.1.16 Ensure that the --audit-log-maxage argument is set to 30 or as appropriate (Scored)
[PASS] 1.1.17 Ensure that the --audit-log-maxbackup argument is set to 10 or as appropriate (Scored)
[PASS] 1.1.18 Ensure that the --audit-log-maxsize argument is set to 100 or as appropriate (Scored)
[PASS] 1.1.19 Ensure that the --authorization-mode argument is not set to AlwaysAllow (Scored)
[PASS] 1.1.20 Ensure that the --token-auth-file parameter is not set (Scored)
[FAIL] 1.1.21 Ensure that the --kubelet-certificate-authority argument is set as appropriate (Scored)
[PASS] 1.1.22 Ensure that the --kubelet-client-certificate and --kubelet-client-key arguments are set as appropriate (Scored)
[PASS] 1.1.23 Ensure that the --service-account-lookup argument is set to true (Scored)
[FAIL] 1.1.24 Ensure that the admission control policy is set to PodSecurityPolicy (Scored)
[PASS] 1.1.25 Ensure that the --service-account-key-file argument is set as appropriate (Scored)
[PASS] 1.1.26 Ensure that the --etcd-certfile and --etcd-keyfile arguments are set as appropriate (Scored
[PASS] 1.1.27 Ensure that the admission control policy is set to ServiceAccount (Scored)
[PASS] 1.1.28 Ensure that the --tls-cert-file and --tls-private-key-file arguments are set as appropriate (Scored)
[PASS] 1.1.29 Ensure that the --client-ca-file argument is set as appropriate (Scored)
[PASS] 1.1.30 Ensure that the --etcd-cafile argument is set as appropriate (Scored)
[PASS] 1.1.31 Ensure that the --authorization-mode argument is set to Node (Scored)
[FAIL] 1.1.32 Ensure that the admission control policy is set to NodeRestriction (Scored)
[FAIL] 1.1.33 Ensure that the --experimental-encryption-provider-config argument is set as appropriate (Scored)
[WARN] 1.1.34 Ensure that the encryption provider is set to aescbc (Scored)
[FAIL] 1.1.35 Ensure that the admission control policy is set to EventRateLimit (Scored)
[WARN] 1.1.36 Ensure that the AdvancedAuditing argument is not set to false (Scored)
[WARN] 1.1.37 Ensure that the --request-timeout argument is set as appropriate (Scored)
[INFO] 1.2 Scheduler
[PASS] 1.2.1 Ensure that the --profiling argument is set to false (Scored)
[INFO] 1.3 Controller Manager
[PASS] 1.3.1 Ensure that the --terminated-pod-gc-threshold argument is set as appropriate (Scored)
[PASS] 1.3.2 Ensure that the --profiling argument is set to false (Scored)
[PASS] 1.3.3 Ensure that the --use-service-account-credentials argument is set
[PASS] 1.3.4 Ensure that the --service-account-private-key-file argument is set as appropriate (Scored)
[PASS] 1.3.5 Ensure that the --root-ca-file argument is set as appropriate (Scored)
[WARN] 1.3.6 Apply Security Context to Your Pods and Containers (Not Scored)
[FAIL] 1.3.7  Ensure that the RotateKubeletServerCertificate argument is set to true (Scored)
[INFO] 1.4 Configuration Files
[PASS] 1.4.1 Ensure that the API server pod specification file permissions are set to 644 or more restrictive (Scored)
[PASS] 1.4.2 Ensure that the API server pod specification file ownership is set to root:root (Scored)
[PASS] 1.4.3 Ensure that the controller manager pod specification file permissions are set to 644 or more restrictive (Scored)
[PASS] 1.4.4 Ensure that the controller manager pod specification file ownership is set to root:root (Scored)
[PASS] 1.4.5 Ensure that the scheduler pod specification file permissions are set to 644 or more restrictive (Scored)
[PASS] 1.4.6 Ensure that the scheduler pod specification file ownership is set to root:root (Scored)
[FAIL] 1.4.7 Ensure that the etcd pod specification file permissions are set to 644 or more restrictive (Scored)
[FAIL] 1.4.8 Ensure that the etcd pod specification file ownership is set to root:root (Scored)
[WARN] 1.4.9 Ensure that the Container Network Interface file permissions are set to 644 or more restrictive (Not Scored)
[WARN] 1.4.10 Ensure that the Container Network Interface file ownership is set to root:root (Not Scored)
[FAIL] 1.4.11 Ensure that the etcd data directory permissions are set to 700 or more restrictive (Scored)
[FAIL] 1.4.12 Ensure that the etcd data directory ownership is set to etcd:etcd (Scored)
[FAIL] 1.4.13 Ensure that the admin.conf file permissions are set to 644 or more restrictive (Scored)
[FAIL] 1.4.14 Ensure that the admin.conf file ownership is set to root:root (Scored)
[PASS] 1.4.15 Ensure that the scheduler.conf file permissions are set to 644 or more restrictive (Scored)
[PASS] 1.4.16 Ensure that the scheduler.conf file ownership is set to root:root (Scored)
[PASS] 1.4.17 Ensure that the controller-manager.conf file permissions are set to 644 or more restrictive (Scored)
[PASS] 1.4.18 Ensure that the controller-manager.conf file ownership is set to root:root (Scored)
[INFO] 1.5 etcd
[PASS] 1.5.1 Ensure that the --cert-file and --key-file arguments are set as appropriate (Scored)
[FAIL] 1.5.2 Ensure that the --client-cert-auth argument is set to true (Scored)
[PASS] 1.5.3 Ensure that the --auto-tls argument is not set to true (Scored)
[PASS] 1.5.4 Ensure that the --peer-cert-file and --peer-key-file arguments are set as appropriate (Scored)
[FAIL] 1.5.5 Ensure that the --peer-client-cert-auth argument is set to true (Scored)
[PASS] 1.5.6 Ensure that the --peer-auto-tls argument is not set to true (Scored)
[FAIL] 1.5.7 Ensure that the --wal-dir argument is set as appropriate (Scored)
[FAIL] 1.5.8 Ensure that the --max-wals argument is set to 0 (Scored)
[PASS] 1.5.9 Ensure that a unique Certificate Authority is used for etcd (Not Scored)
[INFO] 1.6 General Security Primitives
[WARN] 1.6.1 Ensure that the cluster-admin role is only used where required (Not Scored)
[WARN] 1.6.2 Create Pod Security Policies for your cluster (Not Scored)
[WARN] 1.6.3 Create administrative boundaries between resources using namespaces (Not Scored)
[WARN] 1.6.4 Create network segmentation using Network Policies (Not Scored)
[WARN] 1.6.5 Ensure that the seccomp profile is set to docker/default in your pod definitions (Not Scored)
[WARN] 1.6.6 Apply Security Context to Your Pods and Containers (Not Scored)
[WARN] 1.6.7 Configure Image Provenance using ImagePolicyWebhook admission controller (Not Scored)
[WARN] 1.6.8 Configure Network policies as appropriate (Not Scored)
[WARN] 1.6.9 Place compensating controls in the form of PSP and RBAC for privileged containers usage (Not Scored)

== Remediations ==
1.1.6 Edit the API server pod specification file /etc/kubernetes/manifests/kube-apiserver.yaml
apiserver.yaml on the master node and set the below parameter.
--insecure-port=0

1.1.13 Edit the API server pod specification file /etc/kubernetes/manifests/kube-apiserver.yaml
on the master node and set the --admission-control parameter to
include SecurityContextDeny.
--admission-control=...,SecurityContextDeny,...

1.1.21 Follow the Kubernetes documentation and setup the TLS connection between the apiserver
and kubelets. Then, edit the API server pod specification file
/etc/kubernetes/manifests/kube-apiserver.yaml on the master node and set the --
kubelet-certificate-authority parameter to the path to the cert file for the certificate
authority.
--kubelet-certificate-authority=<ca-string>

1.1.24 Follow the documentation and create Pod Security Policy objects as per your environment.
Then, edit the API server pod specification file /etc/kubernetes/manifests/kube-apiserver.yaml
on the master node and set the --admission-control parameter to a
value that includes PodSecurityPolicy :
--admission-control=...,PodSecurityPolicy,...

Then restart the API Server.

1.1.32 Follow the Kubernetes documentation and configure NodeRestriction plug-in on kubelets.
Then, edit the API server pod specification file /etc/kubernetes/manifests/kube-apiserver.yaml
on the master node and set the --admission-control parameter to a
value that includes NodeRestriction.
--admission-control=...,NodeRestriction,...

1.1.33 Follow the Kubernetes documentation and configure a EncryptionConfig file. Then, edit
the API server pod specification file /etc/kubernetes/manifests/kube-apiserver.yaml
on the master node and set the --experimental-encryption-provider-config parameter
to the path of that file:
--experimental-encryption-provider-config=</path/to/EncryptionConfig/File>

1.1.34 Follow the Kubernetes documentation and configure a EncryptionConfig file. In this file,
choose aescbc as the encryption provider.
For example,
kind: EncryptionConfig
apiVersion: v1
resources:
  - resources:
    - secrets
      providers:
      - aescbc:
          keys:
          - name: key1
            secret: <32-byte base64-encoded secret>

1.1.35 Follow the Kubernetes documentation and set the desired limits in a configuration file.
Then, edit the API server pod specification file /etc/kubernetes/manifests/kube-apiserver.yaml
and set the below parameters.
--admission-control=EventRateLimit
--admission-control-config-file=<path/to/configuration/file>

1.1.36 Follow the Kubernetes documentation and set the desired audit policy in the
/etc/kubernetes/audit-policy.yaml file. Then, edit the API server pod specification file /etc/kubernetes/manifests/kube-apiserver.yaml
and set the below parameters.
--audit-policy-file=/etc/kubernetes/audit-policy.yaml

1.1.37 Edit the API server pod specification file /etc/kubernetes/manifests/kube-apiserver.yaml
and set the below parameter as appropriate and if needed. For example,
--request-timeout=300

1.3.6 Follow the Kubernetes documentation and apply security contexts to your pods. For a
suggested list of security contexts, you may refer to the CIS Security Benchmark for Docker
Containers.

1.3.7 Edit the Controller Manager pod specification file /etc/kubernetes/manifests/kube-apiserver.yaml
controller-manager.yaml on the master node and set the --feature-gates parameter to
include RotateKubeletServerCertificate=true.
--feature-gates=RotateKubeletServerCertificate=true

1.4.7 Run the below command (based on the file location on your system) on the master node.
For example,
chmod 644 /etc/kubernetes/manifests/etcd.yaml

1.4.8 Run the below command (based on the file location on your system) on the master node.
For example,
chown root:root /etc/kubernetes/manifests/etcd.yaml

1.4.9 Run the below command (based on the file location on your system) on the master node.
For example,
chmod 644 <path/to/cni/files>

1.4.10 Run the below command (based on the file location on your system) on the master node.
For example,
chown root:root <path/to/cni/files>

1.4.11 On the etcd server node, get the etcd data directory, passed as an argument --data-dir ,
from the below command:
ps -ef | grep etcd
Run the below command (based on the etcd data directory found above). For example,
chmod 700 /var/lib/etcd

1.4.12 On the etcd server node, get the etcd data directory, passed as an argument --data-dir ,
from the below command:
ps -ef | grep etcd
Run the below command (based on the etcd data directory found above). For example,
chown etcd:etcd /var/lib/etcd

1.4.13 Run the below command (based on the file location on your system) on the master node.
For example,
chmod 644 /etc/kubernetes/admin.conf

1.4.14 Run the below command (based on the file location on your system) on the master node.
For example,
chown root:root /etc/kubernetes/admin.conf

1.5.2 Edit the etcd pod specification file /etc/kubernetes/manifests/etcd.yaml on the master
node and set the below parameter.
--client-cert-auth="true"

1.5.5 Edit the etcd pod specification file /etc/kubernetes/manifests/etcd.yaml on the master
node and set the below parameter.
--peer-client-cert-auth=true

1.5.7 Edit the etcd pod specification file /etc/kubernetes/manifests/etcd.yaml on the master
node and set the below parameter.
--wal-dir=</path/to/log/dir>

1.5.8 Edit the etcd pod specification file /etc/kubernetes/manifests/etcd.yaml on the master
node and set the below parameter.
--max-wals=0

1.6.1 Remove any unneeded clusterrolebindings :
kubectl delete clusterrolebinding [name]

1.6.2 Follow the documentation and create and enforce Pod Security Policies for your cluster.
Additionally, you could refer the "CIS Security Benchmark for Docker" and follow the
suggested Pod Security Policies for your environment.

1.6.3 Follow the documentation and create namespaces for objects in your deployment as you
need them.

1.6.4 Follow the documentation and create NetworkPolicy objects as you need them.

1.6.5 Seccomp is an alpha feature currently. By default, all alpha features are disabled. So, you
would need to enable alpha features in the apiserver by passing "--feature-
gates=AllAlpha=true" argument.
Edit the /etc/kubernetes/manifests/kube-apiserver.yaml file on the master node and set the KUBE_API_ARGS
parameter to "--feature-gates=AllAlpha=true"
KUBE_API_ARGS="--feature-gates=AllAlpha=true"
Based on your system, restart the kube-apiserver service. For example:
systemctl restart kube-apiserver.service
Use annotations to enable the docker/default seccomp profile in your pod definitions. An
example is as below:
apiVersion: v1
kind: Pod
metadata:
  name: trustworthy-pod
  annotations:
    seccomp.security.alpha.kubernetes.io/pod: docker/default
spec:
  containers:
    - name: trustworthy-container
      image: sotrustworthy:latest

1.6.6 Follow the Kubernetes documentation and apply security contexts to your pods. For a
suggested list of security contexts, you may refer to the CIS Security Benchmark for Docker
Containers.

1.6.7 Follow the Kubernetes documentation and setup image provenance.

1.6.8 Follow the Kubernetes documentation and setup network policies as appropriate.
For example, you could create a "default" isolation policy for a Namespace by creating a
NetworkPolicy that selects all pods but does not allow any traffic:
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: default-deny
spec:
  podSelector:

1.6.9 Follow Kubernetes documentation and setup PSP and RBAC authorization for your cluster.


== Summary ==
48 checks PASS
18 checks FAIL
15 checks WARN
```

##### node
```
[WARN] Unable to get kubectl version, using default version: 1.6
Reading 1.6 specific configuration file
[INFO] 2 Worker Node Security Configuration
[INFO] 2.1 Kubelet
[FAIL] 2.1.1 Ensure that the --allow-privileged argument is set to false (Scored)
[PASS] 2.1.2 Ensure that the --anonymous-auth argument is set to false (Scored)
[PASS] 2.1.3 Ensure that the --authorization-mode argument is not set to AlwaysAllow (Scored)
[PASS] 2.1.4 Ensure that the --client-ca-file argument is set as appropriate (Scored)
[FAIL] 2.1.5 Ensure that the --read-only-port argument is set to 0 (Scored)
[FAIL] 2.1.6 Ensure that the --streaming-connection-idle-timeout argument is not set to 0 (Scored)
[FAIL] 2.1.7 Ensure that the --protect-kernel-defaults argument is set to true (Scored)
[PASS] 2.1.8 Ensure that the --make-iptables-util-chains argument is set to true (Scored)
[PASS] 2.1.9 Ensure that the --keep-terminated-pod-volumes argument is set to false (Scored)
[PASS] 2.1.10 Ensure that the --hostname-override argument is not set (Scored)
[PASS] 2.1.11 Ensure that the --event-qps argument is set to 0 (Scored)
[FAIL] 2.1.12 Ensure that the --tls-cert-file and --tls-private-key-file arguments are set as appropriate (Scored)
[PASS] 2.1.13 Ensure that the --cadvisor-port argument is set to 0 (Scored)
[INFO] 2.2 Configuration Files
[FAIL] 2.2.1 Ensure that the config file permissions are set to 644 or more restrictive (Scored)
[FAIL] 2.2.2 Ensure that the config file ownership is set to root:root (Scored)
[FAIL] 2.2.3 Ensure that the kubelet file permissions are set to 644 or more restrictive (Scored)
[FAIL] 2.2.4 Ensure that the kubelet file ownership is set to root:root (Scored)
[FAIL] 2.2.5 Ensure that the proxy file permissions are set to 644 or more restrictive (Scored)
[FAIL] 2.2.6 Ensure that the proxy file ownership is set to root:root (Scored)

== Remediations ==
2.1.1 Edit the $config file on each node and set the KUBE_ALLOW_PRIV parameter to "--allow-privileged=false"
2.1.5 Edit the /etc/kubernetes/kubelet.conf file on each node and set the KUBELET_ARGS parameter to "--read-only-port=0"
2.1.6 Edit the /etc/kubernetes/kubelet.conf file on each node and set the KUBELET_ARGS parameter to "--streaming-connection-idle-timeout=<appropriate-timeout-value>"
2.1.7 Edit the /etc/kubernetes/kubelet.conf file on each node and set the KUBELET_ARGS parameter to "--protect-kernel-defaults=true"
2.1.12 Follow the Kubernetes documentation and set up the TLS connection on the Kubelet. Then, edit the /etc/kubernetes/kubelet.conf file on the master node and set the KUBELET_ARGS parameter to include "--tls-cert-file=<path/to/tls-certificate-file>" and "--tls-private-key-file=<path/to/tls-key-file>"
2.2.1 Run the below command (based on the file location on your system) on the each worker node.
For example, chmod 644 $config
2.2.2 Run the below command (based on the file location on your system) on the each worker node.
For example, chown root:root $config
2.2.3 Run the below command (based on the file location on your system) on the each worker node.
For example, chmod 644 /etc/kubernetes/kubelet.conf
2.2.4 Run the below command (based on the file location on your system) on the each worker node.
For example, chown root:root /etc/kubernetes/kubelet.conf
2.2.5 Run the below command (based on the file location on your system) on the each worker node.
For example, chmod 644 proxy
2.2.6 Run the below command (based on the file location on your system) on the each worker node.
For example, chown root:root proxy

== Summary ==
8 checks PASS
11 checks FAIL
0 checks WARN
```

#### Docker Bench Security
```
# ------------------------------------------------------------------------------
# Docker Bench for Security v1.3.4
#
# Docker, Inc. (c) 2015-
#
# Checks for dozens of common best-practices around deploying Docker containers in production.
# Inspired by the CIS Docker Community Edition Benchmark v1.1.0.
# ------------------------------------------------------------------------------

Initializing Thu Apr 26 23:15:43 UTC 2018


[INFO] 1 - Host Configuration
[WARN] 1.1  - Ensure a separate partition for containers has been created
[NOTE] 1.2  - Ensure the container host has been Hardened
[PASS] 1.3  - Ensure Docker is up to date
[INFO]      * Using 18.03.1 which is current
[INFO]      * Check with your operating system vendor for support and security maintenance for Docker
[INFO] 1.4  - Ensure only trusted users are allowed to control Docker daemon
[INFO]      * docker:x:999:azureuser
[WARN] 1.5  - Ensure auditing is configured for the Docker daemon
[WARN] 1.6  - Ensure auditing is configured for Docker files and directories - /var/lib/docker
[WARN] 1.7  - Ensure auditing is configured for Docker files and directories - /etc/docker
[WARN] 1.8  - Ensure auditing is configured for Docker files and directories - docker.service
[WARN] 1.9  - Ensure auditing is configured for Docker files and directories - docker.socket
[WARN] 1.10 - Ensure auditing is configured for Docker files and directories - /etc/default/docker
[WARN] 1.11 - Ensure auditing is configured for Docker files and directories - /etc/docker/daemon.json
[WARN] 1.12 - Ensure auditing is configured for Docker files and directories - /usr/bin/docker-containerd
[WARN] 1.13 - Ensure auditing is configured for Docker files and directories - /usr/bin/docker-runc


[INFO] 2 - Docker daemon configuration
[WARN] 2.1  - Ensure network traffic is restricted between containers on the default bridge
[PASS] 2.2  - Ensure the logging level is set to 'info'
[PASS] 2.3  - Ensure Docker is allowed to make changes to iptables
[PASS] 2.4  - Ensure insecure registries are not used
[PASS] 2.5  - Ensure aufs storage driver is not used
[INFO] 2.6  - Ensure TLS authentication for Docker daemon is configured
[INFO]      * Docker daemon not listening on TCP
[INFO] 2.7  - Ensure the default ulimit is configured appropriately
[INFO]      * Default ulimit doesn't appear to be set
[WARN] 2.8  - Enable user namespace support
[PASS] 2.9  - Ensure the default cgroup usage has been confirmed
[PASS] 2.10 - Ensure base device size is not changed until needed
[WARN] 2.11 - Ensure that authorization for Docker client commands is enabled
[WARN] 2.12 - Ensure centralized and remote logging is configured
[WARN] 2.13 - Ensure operations on legacy registry (v1) are Disabled
[PASS] 2.14 - Ensure live restore is Enabled
[WARN] 2.15 - Ensure Userland Proxy is Disabled
[PASS] 2.16 - Ensure daemon-wide custom seccomp profile is applied, if needed
[PASS] 2.17 - Ensure experimental features are avoided in production
[WARN] 2.18 - Ensure containers are restricted from acquiring new privileges


[INFO] 3 - Docker daemon configuration files
[PASS] 3.1  - Ensure that docker.service file ownership is set to root:root
[PASS] 3.2  - Ensure that docker.service file permissions are set to 644 or more restrictive
[PASS] 3.3  - Ensure that docker.socket file ownership is set to root:root
[PASS] 3.4  - Ensure that docker.socket file permissions are set to 644 or more restrictive
[PASS] 3.5  - Ensure that /etc/docker directory ownership is set to root:root
[PASS] 3.6  - Ensure that /etc/docker directory permissions are set to 755 or more restrictive
[INFO] 3.7  - Ensure that registry certificate file ownership is set to root:root
[INFO]      * Directory not found
[INFO] 3.8  - Ensure that registry certificate file permissions are set to 444 or more restrictive
[INFO]      * Directory not found
[INFO] 3.9  - Ensure that TLS CA certificate file ownership is set to root:root
[INFO]      * No TLS CA certificate found
[INFO] 3.10 - Ensure that TLS CA certificate file permissions are set to 444 or more restrictive
[INFO]      * No TLS CA certificate found
[INFO] 3.11 - Ensure that Docker server certificate file ownership is set to root:root
[INFO]      * No TLS Server certificate found
[INFO] 3.12 - Ensure that Docker server certificate file permissions are set to 444 or more restrictive
[INFO]      * No TLS Server certificate found
[INFO] 3.13 - Ensure that Docker server certificate key file ownership is set to root:root
[INFO]      * No TLS Key found
[INFO] 3.14 - Ensure that Docker server certificate key file permissions are set to 400
[INFO]      * No TLS Key found
[PASS] 3.15 - Ensure that Docker socket file ownership is set to root:docker
[PASS] 3.16 - Ensure that Docker socket file permissions are set to 660 or more restrictive
[PASS] 3.17 - Ensure that daemon.json file ownership is set to root:root
[PASS] 3.18 - Ensure that daemon.json file permissions are set to 644 or more restrictive
[PASS] 3.19 - Ensure that /etc/default/docker file ownership is set to root:root
[PASS] 3.20 - Ensure that /etc/default/docker file permissions are set to 644 or more restrictive


[INFO] 4 - Container Images and Build File
[WARN] 4.1  - Ensure a user for the container has been created
[WARN]      * Running as root: k8s_POD_kubernetes-dashboard-64dcf5784f-8nmbw_kube-system_b7244816-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Running as root: k8s_POD_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Running as root: k8s_POD_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Running as root: k8s_POD_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[NOTE] 4.2  - Ensure that containers use trusted base images
[NOTE] 4.3  - Ensure unnecessary packages are not installed in the container
[NOTE] 4.4  - Ensure images are scanned and rebuilt to include security patches
[WARN] 4.5  - Ensure Content trust for Docker is Enabled
[WARN] 4.6  - Ensure HEALTHCHECK instructions have been added to the container image
[WARN]      * No Healthcheck found: [k8s-gcrio.azureedge.net/hyperkube-amd64:v1.10.1]
[WARN]      * No Healthcheck found: [k8s-gcrio.azureedge.net/kubernetes-dashboard-amd64:v1.8.3]
[WARN]      * No Healthcheck found: [k8s-gcrio.azureedge.net/heapster-amd64:v1.5.1]
[WARN]      * No Healthcheck found: [k8s-gcrio.azureedge.net/k8s-dns-dnsmasq-nanny-amd64:1.14.8]
[WARN]      * No Healthcheck found: [k8s-gcrio.azureedge.net/k8s-dns-kube-dns-amd64:1.14.8]
[WARN]      * No Healthcheck found: [k8s-gcrio.azureedge.net/pause-amd64:3.1]
[WARN]      * No Healthcheck found: [k8s-gcrio.azureedge.net/addon-resizer:1.7]
[WARN]      * No Healthcheck found: [k8s-gcrio.azureedge.net/exechealthz-amd64:1.2]
[PASS] 4.7  - Ensure update instructions are not use alone in the Dockerfile
[NOTE] 4.8  - Ensure setuid and setgid permissions are removed in the images
[INFO] 4.9  - Ensure COPY is used instead of ADD in Dockerfile
[INFO]      * ADD in image history: [k8s-gcrio.azureedge.net/hyperkube-amd64:v1.10.1]
[INFO]      * ADD in image history: [k8s-gcrio.azureedge.net/kubernetes-dashboard-amd64:v1.8.3]
[INFO]      * ADD in image history: [k8s-gcrio.azureedge.net/k8s-dns-dnsmasq-nanny-amd64:1.14.8]
[INFO]      * ADD in image history: [k8s-gcrio.azureedge.net/k8s-dns-kube-dns-amd64:1.14.8]
[INFO]      * ADD in image history: [k8s-gcrio.azureedge.net/pause-amd64:3.1]
[INFO]      * ADD in image history: [k8s-gcrio.azureedge.net/addon-resizer:1.7]
[INFO]      * ADD in image history: [k8s-gcrio.azureedge.net/exechealthz-amd64:1.2]
[NOTE] 4.10 - Ensure secrets are not stored in Dockerfiles
[NOTE] 4.11 - Ensure verified packages are only Installed


[INFO] 5  - Container Runtime
[PASS] 5.1  - Ensure AppArmor Profile is Enabled
[PASS] 5.2  - Ensure SELinux security options are set, if applicable
[PASS] 5.3  - Ensure Linux Kernel Capabilities are restricted within containers
[WARN] 5.4  - Ensure privileged containers are not used
[WARN]      * Container running in Privileged mode: k8s_kube-proxy_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[PASS] 5.5  - Ensure sensitive host system directories are not mounted on containers
[PASS] 5.6  - Ensure ssh is not run within containers
[PASS] 5.7  - Ensure privileged ports are not mapped within containers
[NOTE] 5.8  - Ensure only needed ports are open on the container
[WARN] 5.9  - Ensure the host's network namespace is not shared
[WARN]      * Container running with networking mode 'host': k8s_POD_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[WARN] 5.10 - Ensure memory usage for container is limited
[WARN]      * Container running without memory restrictions: k8s_dnsmasq_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Container running without memory restrictions: k8s_kube-proxy_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Container running without memory restrictions: k8s_POD_kubernetes-dashboard-64dcf5784f-8nmbw_kube-system_b7244816-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Container running without memory restrictions: k8s_POD_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Container running without memory restrictions: k8s_POD_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Container running without memory restrictions: k8s_POD_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[PASS] 5.11 - Ensure CPU priority is set appropriately on the container
[WARN] 5.12 - Ensure the container's root filesystem is mounted as read only
[WARN]      * Container running with root FS mounted R/W: k8s_kubernetes-dashboard_kubernetes-dashboard-64dcf5784f-8nmbw_kube-system_b7244816-48d5-11e8-bcad-000d3a18cdd6_33
[WARN]      * Container running with root FS mounted R/W: k8s_healthz_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_26
[WARN]      * Container running with root FS mounted R/W: k8s_dnsmasq_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Container running with root FS mounted R/W: k8s_heapster-nanny_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Container running with root FS mounted R/W: k8s_kubedns_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_20
[WARN]      * Container running with root FS mounted R/W: k8s_heapster_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Container running with root FS mounted R/W: k8s_kube-proxy_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Container running with root FS mounted R/W: k8s_POD_kubernetes-dashboard-64dcf5784f-8nmbw_kube-system_b7244816-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Container running with root FS mounted R/W: k8s_POD_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Container running with root FS mounted R/W: k8s_POD_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Container running with root FS mounted R/W: k8s_POD_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[PASS] 5.13 -  Ensure incoming container traffic is binded to a specific host interface
[WARN] 5.14 - Ensure 'on-failure' container restart policy is set to '5'
[WARN]      * MaximumRetryCount is not set to 5: k8s_kubernetes-dashboard_kubernetes-dashboard-64dcf5784f-8nmbw_kube-system_b7244816-48d5-11e8-bcad-000d3a18cdd6_33
[WARN]      * MaximumRetryCount is not set to 5: k8s_healthz_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_26
[WARN]      * MaximumRetryCount is not set to 5: k8s_dnsmasq_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * MaximumRetryCount is not set to 5: k8s_heapster-nanny_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * MaximumRetryCount is not set to 5: k8s_kubedns_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_20
[WARN]      * MaximumRetryCount is not set to 5: k8s_heapster_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * MaximumRetryCount is not set to 5: k8s_kube-proxy_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * MaximumRetryCount is not set to 5: k8s_POD_kubernetes-dashboard-64dcf5784f-8nmbw_kube-system_b7244816-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * MaximumRetryCount is not set to 5: k8s_POD_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * MaximumRetryCount is not set to 5: k8s_POD_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * MaximumRetryCount is not set to 5: k8s_POD_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[PASS] 5.15 - Ensure the host's process namespace is not shared
[PASS] 5.16 - Ensure the host's IPC namespace is not shared
[PASS] 5.17 - Ensure host devices are not directly exposed to containers
[INFO] 5.18 - Ensure the default ulimit is overwritten at runtime, only if needed
[INFO]      * Container no default ulimit override: k8s_kubernetes-dashboard_kubernetes-dashboard-64dcf5784f-8nmbw_kube-system_b7244816-48d5-11e8-bcad-000d3a18cdd6_33
[INFO]      * Container no default ulimit override: k8s_healthz_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_26
[INFO]      * Container no default ulimit override: k8s_dnsmasq_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_2
[INFO]      * Container no default ulimit override: k8s_heapster-nanny_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[INFO]      * Container no default ulimit override: k8s_kubedns_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_20
[INFO]      * Container no default ulimit override: k8s_heapster_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[INFO]      * Container no default ulimit override: k8s_kube-proxy_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[INFO]      * Container no default ulimit override: k8s_POD_kubernetes-dashboard-64dcf5784f-8nmbw_kube-system_b7244816-48d5-11e8-bcad-000d3a18cdd6_2
[INFO]      * Container no default ulimit override: k8s_POD_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_2
[INFO]      * Container no default ulimit override: k8s_POD_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[INFO]      * Container no default ulimit override: k8s_POD_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[PASS] 5.19 - Ensure mount propagation mode is not set to shared
[WARN] 5.20 - Ensure the host's UTS namespace is not shared
[WARN]      * Host UTS namespace being shared with: k8s_kube-proxy_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[WARN] 5.21 - Ensure the default seccomp profile is not Disabled
[WARN]      * Default seccomp profile disabled: k8s_kubernetes-dashboard_kubernetes-dashboard-64dcf5784f-8nmbw_kube-system_b7244816-48d5-11e8-bcad-000d3a18cdd6_33
[WARN]      * Default seccomp profile disabled: k8s_healthz_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_26
[WARN]      * Default seccomp profile disabled: k8s_dnsmasq_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Default seccomp profile disabled: k8s_heapster-nanny_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Default seccomp profile disabled: k8s_kubedns_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_20
[WARN]      * Default seccomp profile disabled: k8s_heapster_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Default seccomp profile disabled: k8s_kube-proxy_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Default seccomp profile disabled: k8s_POD_kubernetes-dashboard-64dcf5784f-8nmbw_kube-system_b7244816-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Default seccomp profile disabled: k8s_POD_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Default seccomp profile disabled: k8s_POD_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Default seccomp profile disabled: k8s_POD_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[NOTE] 5.22 - Ensure docker exec commands are not used with privileged option
[NOTE] 5.23 - Ensure docker exec commands are not used with user option
[WARN] 5.24 - Ensure cgroup usage is confirmed
[WARN]      * Confirm cgroup usage: k8s_kubernetes-dashboard_kubernetes-dashboard-64dcf5784f-8nmbw_kube-system_b7244816-48d5-11e8-bcad-000d3a18cdd6_33
[WARN]      * Confirm cgroup usage: k8s_healthz_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_26
[WARN]      * Confirm cgroup usage: k8s_dnsmasq_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Confirm cgroup usage: k8s_heapster-nanny_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Confirm cgroup usage: k8s_kubedns_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_20
[WARN]      * Confirm cgroup usage: k8s_heapster_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Confirm cgroup usage: k8s_kube-proxy_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Confirm cgroup usage: k8s_POD_kubernetes-dashboard-64dcf5784f-8nmbw_kube-system_b7244816-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Confirm cgroup usage: k8s_POD_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Confirm cgroup usage: k8s_POD_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Confirm cgroup usage: k8s_POD_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[WARN] 5.25 - Ensure the container is restricted from acquiring additional privileges
[WARN]      * Privileges not restricted: k8s_kubernetes-dashboard_kubernetes-dashboard-64dcf5784f-8nmbw_kube-system_b7244816-48d5-11e8-bcad-000d3a18cdd6_33
[WARN]      * Privileges not restricted: k8s_healthz_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_26
[WARN]      * Privileges not restricted: k8s_dnsmasq_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Privileges not restricted: k8s_heapster-nanny_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Privileges not restricted: k8s_kubedns_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_20
[WARN]      * Privileges not restricted: k8s_heapster_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Privileges not restricted: k8s_kube-proxy_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Privileges not restricted: k8s_POD_kubernetes-dashboard-64dcf5784f-8nmbw_kube-system_b7244816-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Privileges not restricted: k8s_POD_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Privileges not restricted: k8s_POD_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Privileges not restricted: k8s_POD_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[WARN] 5.26 - Ensure container health is checked at runtime
[WARN]      * Health check not set: k8s_kubernetes-dashboard_kubernetes-dashboard-64dcf5784f-8nmbw_kube-system_b7244816-48d5-11e8-bcad-000d3a18cdd6_33
[WARN]      * Health check not set: k8s_healthz_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_26
[WARN]      * Health check not set: k8s_dnsmasq_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Health check not set: k8s_heapster-nanny_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Health check not set: k8s_kubedns_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_20
[WARN]      * Health check not set: k8s_heapster_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Health check not set: k8s_kube-proxy_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Health check not set: k8s_POD_kubernetes-dashboard-64dcf5784f-8nmbw_kube-system_b7244816-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Health check not set: k8s_POD_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Health check not set: k8s_POD_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * Health check not set: k8s_POD_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[INFO] 5.27 - Ensure docker commands always get the latest version of the image
[WARN] 5.28 - Ensure PIDs cgroup limit is used
[WARN]      * PIDs limit not set: k8s_kubernetes-dashboard_kubernetes-dashboard-64dcf5784f-8nmbw_kube-system_b7244816-48d5-11e8-bcad-000d3a18cdd6_33
[WARN]      * PIDs limit not set: k8s_healthz_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_26
[WARN]      * PIDs limit not set: k8s_dnsmasq_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * PIDs limit not set: k8s_heapster-nanny_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * PIDs limit not set: k8s_kubedns_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_20
[WARN]      * PIDs limit not set: k8s_heapster_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * PIDs limit not set: k8s_kube-proxy_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * PIDs limit not set: k8s_POD_kubernetes-dashboard-64dcf5784f-8nmbw_kube-system_b7244816-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * PIDs limit not set: k8s_POD_kube-dns-v20-59b4f7dc55-wmbkl_kube-system_b6eb8ef4-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * PIDs limit not set: k8s_POD_heapster-568476f785-4fg4p_kube-system_c1c26ad6-48d5-11e8-bcad-000d3a18cdd6_2
[WARN]      * PIDs limit not set: k8s_POD_kube-proxy-mqcqf_kube-system_b70dcbc1-48d5-11e8-bcad-000d3a18cdd6_2
[PASS] 5.29 - Ensure Docker's default bridge docker0 is not used
[PASS] 5.30 - Ensure the host's user namespaces is not shared
[PASS] 5.31 - Ensure the Docker socket is not mounted inside any containers


[INFO] 6 - Docker Security Operations
[INFO] 6.1  - Avoid image sprawl
[INFO]      * There are currently: 8 images
[INFO] 6.2  - Avoid container sprawl
[INFO]      * There are currently a total of 21 containers, with 11 of them currently running


[INFO] 7 - Docker Swarm Configuration
[PASS] 7.1  - Ensure swarm mode is not Enabled, if not needed
[PASS] 7.2  - Ensure the minimum number of manager nodes have been created in a swarm (Swarm mode not enabled)
[PASS] 7.3  - Ensure swarm services are binded to a specific host interface (Swarm mode not enabled)
[PASS] 7.5  - Ensure Docker's secret management commands are used for managing secrets in a Swarm cluster (Swarm mode not enabled)
[PASS] 7.6  - Ensure swarm manager is run in auto-lock mode (Swarm mode not enabled)
[PASS] 7.7  - Ensure swarm manager auto-lock key is rotated periodically (Swarm mode not enabled)
[PASS] 7.8  - Ensure node certificates are rotated as appropriate (Swarm mode not enabled)
[PASS] 7.9  - Ensure CA certificates are rotated as appropriate (Swarm mode not enabled)
[PASS] 7.10 - Ensure management plane traffic has been separated from data plane traffic (Swarm mode not enabled)

[INFO] Checks: 104
[INFO] Score: 15
```

### Going Forward
TODO: Document remediations here