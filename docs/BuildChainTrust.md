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
Based on [kubernetes/kubernetes #30603](https://github.com/kubernetes/kubernetes/issues/30603) and [kubernetes/kubernetes #22888](https://github.com/kubernetes/kubernetes/issues/22888#issuecomment-210566037), it should be possible for kubernetes to verify image signatures however this capability is not provided out of the box.

### Going Forward
Export `DOCKER_CONTENT_TRUST=1` today when pushing images, which will automaically create keys and signed images if pushing Docker Hub. If using private registries and ACR, use image signing feature when it becomes available.

TODO: Provide example of an [ImagePolicyWebhook](https://kubernetes.io/docs/admin/admission-controllers/#imagepolicywebhook) implementation that enables content trust verifications

