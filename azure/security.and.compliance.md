# Security and Compliance

## Azure Security Center

Centralized security management for Azure resources. 
- protects your Azure resources against threats
- personalizes security recommendations based on your environment
- analyzing potential threats and vulnerabilities
- increased security through JIT - Just in Time access
  
**Secure Score** is a measure of the security posture of your Azure environment. It is a composite score that is calculated based on the security configuration of your Azure resources. The score ranges from 0 to 100, with 100 being the most secure. The score is calculated based on the following factors:
- Identity
- Infrastructure
- Apps and data
- ...

**Azure Defender** - a unified security solution that provides advanced threat protection across your hybrid cloud workloads. It provides a single pane of glass to manage security across your Azure and non-Azure workloads. It provides the following capabilities:


## Security Components

- **Defense in Depth** - multiple layers of security, control, protection
- **Firewalls** - network security devices that monitor and control incoming and outgoing network traffic based on predetermined security rules
- **Network Security** - a set of controls that protect the network infrastructure
- **Sentinels** - a set of controls that protect the network infrastructure. Provides intelligent monitoring and alerting for your Azure resources.
- **Key Vault** - a cloud-based service that provides a secure storage of keys, secrets, and certificates.
- **Network Security Groups (NSG)** - a set of security rules that allow or deny inbound and outbound network traffic based on source or destination IP address, port, and protocol.
- ...


## Security Posture

**Security Posture** is the state of security of an organization. It is a measure of the security of an organization. It is a composite score that is calculated based on the security configuration of your Azure resources. The score ranges from 0 to 100, with 100 being the most secure. 
 - budget/resources spent on security
 - understanding of shared responsibility model
 - policies and documentation

A **defense in depth model - DID** - is that which seeks to apply protections at various levels:
 - physical
 - Network
 - Data
 - Host
 - Application
   
  Protection of data at rest, in transit, and in use.
  - Data at rest - encryption - AES - Advanced Encryption Standard
  - Data in transit - TLS - Transport Layer Security
  - Data is use - RBAC - Role Based Access Control

## Azure dedicated hosts

**Dedicated hosts** are physical servers with Azure guest VMs. They are **dedicated to a single customer** and can be used to host VMs with specific software licensing requirements. They are ideal for customers who want to use their existing server-bound software licenses on Azure. They are also ideal for customers who want to use single-tenant hardware for security and compliance reasons.

### Network Security Groups (NSG)

**Network Security Groups (NSG)** are a set of security rules that allow or deny inbound and outbound network traffic based on source or destination IP address, port, and protocol. They are applied to a subnet, a virtual network, or a network interface. They are stateful, meaning that return traffic for allowed inbound traffic is automatically allowed, even if a specific rule for return traffic doesn't exist. They are also hierarchical, meaning that a security rule can be applied to a subnet, which can be applied to a virtual network, which can be applied to a network interface.

### Azure Firewall

**Azure Firewall** is a managed, cloud-based network security service that protects your Azure Virtual Network resources. It is a **layer 3-4** firewall that provides **stateful filtering** of **inbound** and **outbound** network traffic to and from Azure resources. It is a **next-generation firewall** that is **highly available** and **scalable**. It is **transparent** to your virtual machines and is **integrated** with Azure Monitor for logging and alerting. It is **automated** and **provisioned** through the Azure portal, Azure PowerShell, and Azure CLI. 

### Azure Sentinel - Security Information and Event Management (SIEM)

**Azure Sentinel** is a cloud-native SIEM and security analytics service that provides intelligent security analytics and threat intelligence across the enterprise, providing a single solution for alert detection, threat visibility, proactive hunting, and threat response. It is a **unified security management** and **analytics** platform that **connects** data from **multiple sources** and **provides** a **single pane of glass** to **manage** security across your Azure and non-Azure workloads. It provides the following capabilities:


### Key Vault

**Key Vault** is a cloud-based service that provides a secure storage of keys, secrets, and certificates. It is a **managed service** that is **automated** and **provisioned** through the Azure portal, Azure PowerShell, and Azure CLI. It is **transparent** to your virtual machines and is **integrated** with Azure Monitor for logging and alerting. It is **automated** and **provisioned** through the Azure portal, Azure PowerShell, and Azure CLI.

## Governance

Governance typically refers to the application of best practices, policies and procedures by a governing body.

In IT it refers to the application of best practices, policies and procedures by a governing body to ensure that IT resources are used in a way that is consistent with the organization's goals and objectives.


### Resource Locks 

**Resource Locks** protects against the **accidental deletion** of resources. They are applied to a resource group, a resource, or a subscription. They are hierarchical, meaning that a lock can be applied to a resource group, which can be applied to a resource, which can be applied to a subscription. They are **automated** and **provisioned** through the Azure portal, Azure PowerShell, and Azure CLI.

### Policy

**Policy** is a set of rules that are applied to a resource group, a resource, or a subscription. They are hierarchical, meaning that a policy can be applied to a resource group, which can be applied to a resource, which can be applied to a subscription. They are **automated** and **provisioned** through the Azure portal, Azure PowerShell, and Azure CLI.

### Role Based Access Control (RBAC)

**Role Based Access Control (RBAC)** is a set of rules that are applied to a resource group, a resource, or a subscription. They are hierarchical, meaning that a policy can be applied to a resource group, which can be applied to a resource, which can be applied to a subscription. They are **automated** and **provisioned** through the Azure portal, Azure PowerShell, and Azure CLI.

## Security and Compliance Offerings

- Security
- Privacy
- Compliance

Compliance Center:
 - NIST
 - HIPAA
 - CJIS

##  Trust Center

 - Privacy statements
 - Online services terms
 - Data protection
 - Compliance terms and requirements





