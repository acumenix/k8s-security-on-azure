## Encrypt persistent volume
### Context
Azure offers several mechanism for data encryption:
- ADE: [Azure Disk Encryption](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)

    Azure Disk Encryption allows you to encrypt the OS and Data disks used by an IaaS Virtual Machine. This includes managed disks. For Windows, the drives are encrypted using industry-standard BitLocker encryption technology. For Linux, the disks are encrypted using the DM-Crypt technology. This is integrated with Azure Key Vault to allow you to control and manage the disk encryption keys.

- SSE: [Storage Service Encryption](https://docs.microsoft.com/en-us/azure/storage/common/storage-service-encryption)

    Azure Disk Encryption allows you to encrypt the OS and Data disks used by an IaaS Virtual Machine. This includes managed disks. As of June 10, 2017, new data written to existing managed disks is automatically encrypted.

The purpose of this article is to describe what is available today in terms of storage encryption for Kubernetes clusters runing in Azure with AKS or ACS-Engine.

### Current State
There is no plan to add support for ADE before v1.11 based on the comments in [issue #747 on acs-engine](https://github.com/Azure/acs-engine/issues/747)

SSE is supported natively with the default behavior of managed disks. There is no support for the use of custom keys to do SSE encryption.

### Going Forward
TODO: add support for SSE with custom keys

...
