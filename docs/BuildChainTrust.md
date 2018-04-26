## Build chain & content trust
### Context
Out of the box, Docker images pulled from a repository are not signed and thus vulnerable to manipulation via man-in-the-middle attacks if a malicious attacker can intercept network traffic.

There are two aspects to this issue:

1. Image signing (typically during image push),
2. Image verification (typically on cluster during image pull)

### Current State
#### Image Signing
A framework for image signing exists upstream and is outlined in great detail in the [Docker Content Trust](https://docs.docker.com/engine/security/trust/content_trust/) documentation. Setting environment variable `DOCKER_CONTENT_TRUST=1` while building and pushing images will enable the content trust features.

Per the [Azure Container Registry Roadmap](https://github.com/Azure/acr/blob/master/docs/acr-roadmap.md#trusted-registries), ACR has plans to support content trust as well which will allow signing of images to your private Azure registry.

A limitation of the Docker Content Trust framework is that *images* are not actually signed; the tag+image SHA is and that metadata is offloaded (e.g. to a Notary instance).

Therefore, for establishing content trust your registry must support serving the content trust metadata in order for the pulling party to verify an image, and this signature is does not move with the image if you push it to another repository or copy it offline.

#### Image Verification
Verification side of things is in a very rough state.

##### Docker CE Version
Firstly, Docker Content Trust is available starting with Docker CE 18.03+, and acs-engine defaults to docker-engine 1.13 and even only supports up to 17.05 when overriding the engine version.

As a result, Docker CE must manually be provisioned on the master/agents:
```
# Change use of docker daemon -> dockerd
sudo sed -i -e 's/docker daemon/dockerd/' /etc/systemd/system/docker.service.d/exec_start.conf

# Grab from Docker repos per upstream docs
sudo apt-get update
sudo apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update
sudo apt-get install -y docker-ce
```

##### Content trust via pull API
Even once the updated Docker CE is installed and content trust is available for the CLI, there is currently no mechanism provided by Docker nor Moby upstream to enable content trust via the Go SDK/API interfaces (which Kubernetes uses to pull images). A good summary of the current state is provided in [moby/moby #27511](https://github.com/moby/moby/issues/27511), and this feature is tracked by upstream issue [moby/moby #16654](https://github.com/moby/moby/issues/16654).

Based on [kubernetes/kubernetes #30603](https://github.com/kubernetes/kubernetes/issues/30603) and [kubernetes/kubernetes #22888](https://github.com/kubernetes/kubernetes/issues/22888#issuecomment-210566037), it may be possible for kubernetes to verify image signatures using a imagePolicyWebhook, however this capability is not provided out of the box and must be implemented manually, duplicating upstream Docker functionality.

The relevant image-pull code that requires modification can be found here:
*  [kubernetes (kube_docker_client.go)](https://github.com/kubernetes/kubernetes/blob/915798d229b7be076d8e53d6aa1573adabd470d2/pkg/kubelet/dockershim/libdocker/kube_docker_client.go#L360)
* [go-docker](https://github.com/docker/go-docker/blob/master/image_pull.go#L21)

*Note - k8s still imports the deprecated client `github.com/docker/docker/client`, updated client by name of `docker.io/go-docker` is linked above.*


### Going Forward
Export `DOCKER_CONTENT_TRUST=1` today when pushing images, which will automaically create keys and signed images if pushing Docker Hub. If using private registries and ACR, use image signing feature when it becomes available.

TODO: Provide example of an [ImagePolicyWebhook](https://kubernetes.io/docs/admin/admission-controllers/#imagepolicywebhook) implementation that enables content trust verifications

