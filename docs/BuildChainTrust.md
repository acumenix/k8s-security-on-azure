## Build chain & content trust
### Context
Out of the box, Docker images pulled from a repository are not signed and thus vulnerable to manipulation via man-in-the-middle attacks if a malicious attacker can intercept network traffic.

There are two aspects to this issue:

1. Image signing (typically during image push),
2. Image verification (typically on cluster during image pull)

