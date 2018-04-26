## Auditing policy
### Context
Kubernetes auditing is a feature of the API server that provides an audit trail of events initiated by users and actions affecting components of the cluster. Upstream documentation is available [here](https://kubernetes.io/docs/tasks/debug-application-cluster/audit/).

### Current State
Auditing policy is now enabled by default in acs-engine, but the policy cannot be altered via parameters. Uploading a new audit policy to `/etc/kubernetes/audit-policy.yaml` should trigger a restart the API server automatically.

### Going Forward
TODO: PR to acs-engine for customizable policies.

See also current bug [azure/acs-engine #2312](https://github.com/Azure/acs-engine/issues/2312)