## Vulnerability scanning
### Context
When building Docker images from other base images, it is important to ensure that the referenced image layers do not contain any known vulnerabilities.

Even when building containers from scratch new vulnerabilities may be discovered that affecting your application's dependencies and render ane existing container build vulnerable.

Vulnerability scanners help identify and remediate these issues by scanning for well-known vulnerabilities.


### Current State
Examples of open-source solutions:
* [Clair](https://github.com/coreos/clair)
* [Dagda](https://github.com/eliasgranderubio/dagda)

Examples of commercial solutions:
* [AquaSec](https://www.aquasec.com/products/aqua-container-security-platform/) [Also available via [Azure Marketplace offering](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/aqua-security.aquasec-csp-2_5?tab=Overview)]
* [Twistlock](https://www.twistlock.com) [Also available via [Azure Marketplace offering](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/twistlock.twistlock?tab=Overview)]

### Going Forward
TODO: Provide setup scripts