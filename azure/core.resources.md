# Azure Core Resources 

Core resources are the **fundamental building blocks** of Azure. They are the foundation of all other Azure services and are used to build IaaS, PaaS solutions.

Resources examples:

 - **Virtual Machines** are the building blocks of IaaS solutions.
 - **Storage Accounts** are the building blocks of PaaS solutions.
 - **Virtual Networks** are the building blocks of hybrid solutions.
 - **Azure Active Directory** is the building blocks of identity solutions.
 - **Subscriptions** are the building blocks of billing solutions.

Architectural components examples:

 - **Resource Groups** are the building blocks of Azure management solutions.
 - **Regions and Region Pairs** are the building blocks of Azure availability solutions.
 - **Availability Options** are the building blocks of Azure availability solutions.

## Azure Subscriptions

Azure **Subscriptions** are the **fundamental building blocks** of Azure management solutions. They are the **foundation** of all other Azure services and are used to build IaaS, PaaS solutions.

Azure **Subscriptions** are **logical containers** that **group** related **resources**. They are **used** to **manage** access to those resources. **Subscriptions** are **associated** with an **Azure account**.

**Azure account** is a **unique** **identity** that **represents** a **person** or an **organization**. It is **used** to **access** **Azure services**.

## Resource Groups

Azure **Resource Groups** act as containers for Azure resources. They are used to **organize** and **manage** resources in Azure. Resources in a resource group can be **accessed** as a **group** or **individually**.

- rights can be given at the resource group level. Rights to a resource group **automatically** apply to all resources in the group. The rights are to **view**, **manage**, or **delete**, **deploy**, ... resources in the group.
  
- a resource can exist **only** in a single resource group. A resource can be moved from one resource group to another.

- each resource group is associated with a **location**. A location is a **physical** **region** in the world where **Azure** **datacenters** are located. A resource group can only contain resources located in the same location as the resource group.

## ARM - Azure Resource Manager

Azure Resource Manager (ARM) is the **deployment** and **management** **service** for **Azure**. It provides a **management** **layer** that **enables** users to **create**, **update**, and **delete** **resources** in **Azure**.

- organize resources into **resource groups**.
- controls access to resources.
- the ARM is accessed through:
   - the Azure portal
   - the Azure CLI
   - PowerShell
   - and the Azure SDKs. (C#, Java, JavaScript, Python, Go, .NET, Ruby, PHP, ...) and are REST APIs.

## Azure Regions and Region Pairs

### Regions

Azure **Regions** are **physical** **locations** in the world where **Azure** **datacenters** are located. Each region is a **separate** **geographic** **area**. Each region is made up of one or more **datacenters** **equipped** with **power** and **cooling** and connected by a **low-latency** **network**.

 - preserve the **data residency** of the data.
 - provide flexibility and low latency bases on customer location.

### Region Pairs

Azure **Region Pairs** are **pairs** of **regions** that are **physically** **close** to **each other**. They are **used** to **provide** **high availability** for **Azure** **services**. A **region pair** is **composed** of **two** **regions** that are **physically** **close** to **each other**. A **region pair** is **composed** of **two** **regions** that are **physically** **close** to **each other**.

 - at least 300 miles apart
 - provide automatic replication of data between the two regions
 - provide automatic failover of services between the two regions
 - move resources between paired regions


## Availability Options

- **single VMs** - single VMs are not highly available. If the VM fails, the application is not available.

- **availability zones** - availability zones are a **set** of **isolated** **datacenters** within an **Azure** **region**. Each zone is made up of one or more **datacenters** **equipped** with **power** and **cooling** and connected by a **low-latency** **network**. Each zone is **connected** to **other** **zones** in the **same** **region** through a **high-speed** **network**.
  - protects against datacenters failures
  - physically separated datacenters within a region
  - data centers connected by a fast network

- **region pairs**
  - provides multi-region disaster recovery


## Compute Resources

Compute resources are those resources on-demand that provide CPU power, disk and memory storage, networking capabilities and operating systems.

The most common example of **Compute resources** are **Virtual Machines**.


## Storage Resources

**Storage resources** are those resources on-demand that provide disk and memory storage.
The most common example of **Storage resources** are **Storage Accounts**.

- **Storage accounts** are **used** to **store** **data** of **various** **types** (blobs, files, tables, queues, disks, snapshots, backups, ...). **Storage accounts** are **used** to **support** **other** **Azure** **services** (Azure SQL Database, Azure Cosmos DB, Azure Data Lake Storage, Azure HDInsight, Azure Data Factory, Azure Stream Analytics, Azure Machine Learning, Azure Search, Azure IoT Hub, Azure Databricks, Azure Synapse Analytics, ...).

- **Containers** are **used** to **organize** **blobs** and **files** within **storage accounts**.

- **Disk storage** is **used** to **store** **virtual machine disks**.

- **Azure Files** are **used** to **share** **files** between **virtual machines** and **on-premises** **servers**.

- **Storage Tiers** are **used** to **store** **data** at **different** **costs** and **performance** levels.
   - hot storage
   - cool storage
   - archive storage

A **storage account** provides a **unique namespace** for your Azure Storage data that's accessible from anywhere in the world over HTTP or HTTPS. Data in this account is secure, highly available, durable, and massively scalable.

One of the benefits of using an Azure Storage Account is having a unique namespace in Azure for your data. In order to do this, every storage account in Azure must have a unique-in-Azure account name. The combination of the account name and the Azure Storage service endpoint forms the endpoints for your storage account.

Azure Storage always stores multiple copies of your data so that it's protected from planned and unplanned events such as transient hardware failures, network or power outages, and natural disasters. Redundancy ensures that your storage account meets its availability and durability targets even in the face of failures.

### Redundancy in Primary Region

Data in an **Azure Storage account** is always replicated **three times** in the primary region. Azure Storage offers two options for how your data is replicated in the primary region, **locally redundant storage (LRS)** and **zone-redundant storage (ZRS)**.

**Locally redundant storage (LRS)** replicates your data three times within a single data center in the primary region. LRS provides at least 11 nines of durability (99.999999999%) of objects over a given year.

For Availability Zone-enabled Regions, **zone-redundant storage (ZRS)** replicates your Azure Storage data synchronously a**cross three Azure availability zones in the primary region**. ZRS offers durability for Azure Storage data objects of at least 12 nines (99.9999999999%) over a given year. 
With ZRS, your data is still **accessible for both read and write** operations even if a zone becomes unavailable.

### Redundancy in a secondary region

If the data in your storage account is copied to a secondary region, then your data is durable even in the event of a catastrophic failure that prevents the data in the primary region from being recovered.
When you create a storage account, you select the primary region for the account. The paired secondary region is based on** Azure Region Pairs**, and can't be changed.

Azure Storage offers two options for copying your data to a secondary region: 
- **geo-redundant storage (GRS)** - is similar to running LRS in two regions.
- **geo-zone-redundant storage (GZRS)** - is similar to running ZRS in the primary region and LRS in the secondary region.

**By default**, data in the secondary region isn't available for read or write access unless there's a failover to the secondary region. If the primary region becomes unavailable, you can choose to fail over to the secondary region. After the failover has completed, the secondary region becomes the primary region, and you can again read and write data.

**GRS** copies your data synchronously three times within a single physical location in the primary region using LRS. It then copies your data asynchronously to a single physical location in the secondary region (the region pair) using LRS. GRS offers durability for Azure Storage data objects of at least 16 nines (99.99999999999999%) over a given year.

**GZRS** combines the high availability provided by redundancy across availability zones with protection from regional outages provided by geo-replication. Data in a GZRS storage account is copied across three Azure availability zones in the primary region (similar to ZRS) and is also replicated to a secondary geographic region, using LRS, for protection from regional disasters. Microsoft recommends using GZRS for applications requiring maximum consistency, durability, and availability, excellent performance, and resilience for disaster recovery.

Geo-redundant storage (with GRS or GZRS) replicates your data to another physical location in the secondary region to protect against regional outages. However, that data is available to be read only if the customer or Microsoft initiates a failover from the primary to secondary region. However, if you enable read access to the secondary region, your data is always available, even when the primary region is running optimally. For **read access to the secondary region**, enable **read-access geo-redundant storage (RA-GRS) or read-access geo-zone-redundant storage (RA-GZRS)**.

### Azure Storage Services

The Azure Storage platform includes the following data services:

- **Azure Blobs**: A massively scalable object store for text and binary data. Also includes support for big data analytics through Data Lake Storage Gen2.
- **Azure Files**: Managed file shares for cloud or on-premises deployments.
- **Azure Queues**: A messaging store for reliable messaging between application components.
- **Azure Disks**: Block-level storage volumes for Azure VMs.


### Azure Blobs

**Azure Blob Storage** is an object storage solution for the cloud. It can store massive amounts of data, such as text or binary data. Azure Blob Storage is unstructured, meaning that there are no restrictions on the kinds of data it can hold. Blob Storage can manage thousands of simultaneous uploads, massive amounts of video data, constantly growing log files, and can be reached from anywhere with an internet connection.

Objects in Blob storage can be accessed from anywhere in the world via HTTP or HTTPS. Users or client applications can access blobs via URLs, the Azure Storage REST API, Azure PowerShell, Azure CLI, or an Azure Storage client library. The storage client libraries are available for multiple languages, including .NET, Java, Node.js, Python, PHP, and Ruby.

Azure Storage offers different access tiers for your blob storage, helping you store object data in the most cost-effective manner. The available access tiers include:
- **Hot access tier**: Optimized for storing data that is accessed frequently (for example, images for your website).
- **Cool access tier**: Optimized for data that is infrequently accessed and stored for at least 30 days (for example, invoices for your customers).
- **Archive access tier**: Appropriate for data that is rarely accessed and stored for at least 180 days, with flexible latency requirements (for example, long-term backups).

considerations: 

- **Only the hot and cool access tiers** can be set at the account level. - The archive access tier isn't available at the account level.
Hot, cool, and archive tiers can be set at the blob level, **during or after upload**.
- For cool data, a slightly lower availability service-level agreement (SLA) and higher access costs compared to hot data are acceptable trade-offs for lower storage costs.
- Archive storage stores data offline and offers the lowest storage costs, but also the highest costs to rehydrate and access data.

### Azure Files

**Azure Files** offers fully managed file shares in the cloud that are accessible via the industry standard **Server Message Block (SMB)** or **Network File System (NFS)** protocols. Azure Files file shares can be mounted concurrently by cloud or on-premises deployments. SMB Azure file shares are accessible from Windows, Linux, and macOS clients. NFS Azure Files shares are accessible from Linux or macOS clients. Additionally, SMB Azure file shares can be cached on Windows Servers with Azure File Sync for fast access near where the data is being used.

### Queue Storage

**Azure Queue Storage** is a service for storing large numbers of messages. Once stored, you can access the messages from anywhere in the world via authenticated calls using **HTTP or HTTPS**. A queue can contain as many messages as your storage account has room for (potentially millions). **Each individual message can be up to 64 KB in size**. Queues are commonly used to create a backlog of work to process asynchronously.

### Disk Storage

Disk storage, or Azure managed disks, are block-level storage volumes managed by Azure for use with Azure VMs. Conceptually, they’re the same as a physical disk, but they’re virtualized – offering greater resiliency and availability than a physical disk. With managed disks, all you have to do is provision the disk, and Azure will take care of the rest.



## Networking Resources

**Networking resources** are those resources on-demand that provide networking capabilities.

The most common example of **Networking resources** are **Virtual Networks**.

- **Virtual Networks (vNet)** are used to connect Azure resources to **each other**, to **on-premises** resources, and over the Internet. They provide a secure network connection between **resources**.

  Azure virtual networking supports both public and private endpoints to enable communication between external or internal resources with other internal resources.
  - **Public endpoints** have a public IP address and can be accessed from anywhere in the world.
  - **Private endpoints** exist within a virtual network and have a private IP address from within the address space of that virtual network.

Azure virtual networks provide the following key networking capabilities:
  - **Isolation and segmentation** - Azure virtual network allows you to create multiple isolated virtual networks. When you set up a virtual network, you define a **private IP address space** by using either public or private IP address ranges. The IP range only exists within the virtual network and isn't internet routable. You can **divide that IP address space into subnets** and allocate part of the defined address space to each **named subnet**. For **name resolution**, you can use the name resolution service that's built into Azure. You also can configure the virtual network to use either an internal or an external DNS server.

  - **Internet communications** - You can enable incoming connections from the internet by assigning a **public IP address** to an Azure resource, or putting the resource behind a **public load balancer**.

  - **Communicate between Azure resources** 
    - **Virtual networks **can connect not only VMs but other Azure resources, such as the App Service Environment for Power Apps, Azure Kubernetes Service, and Azure virtual machine scale sets. 
    - **Service endpoints** can connect to other Azure resource types, such as Azure SQL databases and storage accounts. This approach enables you to **link multiple Azure resources to virtual networks** to improve security and provide optimal routing between resources.

  - **Communicate with on-premises resources** - Azure virtual networks enable you to link resources together in your on-premises environment and within your Azure subscription.  In effect, you can create a network that spans both your local and cloud environments. There are three mechanisms for you to achieve this connectivity:
    - **Point-to-site** virtual private network connections are from a computer outside your organization back into your corporate network. In this case, the client computer initiates an encrypted VPN connection to connect to the Azure virtual network.
    - **Site-to-site** virtual private networks link your on-premises VPN device or gateway to the Azure VPN gateway in a virtual network. In effect, the devices in Azure can appear as being on the local network. The connection is encrypted and works over the internet.
    - **Azure ExpressRoute** provides a dedicated private connectivity to Azure that doesn't travel over the internet. ExpressRoute is useful for environments where you need greater bandwidth and even higher levels of security.

  - **Route network traffic** - By default, Azure routes traffic between subnets on any connected virtual networks, on-premises networks, and the internet. You also can control routing and override those settings, as follows:
    - **Route tables** allow you to define rules about how traffic should be directed. 
    - **Border Gateway Protocol (BGP)** 

  - **Filter network traffic** - Azure virtual networks enable you to filter traffic between subnets by using the following approaches:
    - **Network security groups** are Azure resources that can contain multiple inbound and outbound security rules. 
    - **Network virtual appliances** are specialized VMs that can be compared to a hardened network appliance. A network virtual appliance carries out a particular network function, such as running a firewall or performing wide area network (WAN) optimization.
   
  - **Connect virtual networks** - You can link virtual networks together by using virtual network peering. Peering allows two virtual networks to connect directly to each other. Network traffic between peered networks is private, and travels on the Microsoft backbone network, never entering the public internet.** User-defined routes (UDR)** allow you to control the routing tables between subnets within a virtual network or between virtual networks. This allows for greater control over network traffic flow.

- **VPN Gateway** is used to connect **on-premises** **networks** to **Azure** **virtual networks** over **Site-to-Site** **VPN** connections.
S2S - Site-to-Site VPN
P2S - Point-to-Site VPN

- **ExpressRoute** is used to create **private** connections between **Azure** and **on-premises** **networks**.

### Azure VPN

A **virtual private network (VPN)** uses an encrypted tunnel within another network. VPNs are typically deployed to connect two or more trusted private networks to one another over an untrusted network (typically the public internet). Traffic is encrypted while traveling over the untrusted network to prevent eavesdropping or other attacks. VPNs can enable networks to safely and securely share sensitive information.

### VPN Gateways

A VPN gateway is a type of virtual network gateway. Azure VPN Gateway instances are deployed in a dedicated subnet of the virtual network and enable the following connectivity:

- Connect on-premises datacenters to virtual networks through a site-to-site connection.

- Connect individual devices to virtual networks through a point-to-site connection.
  
- Connect virtual networks to other virtual networks through a network-to-network connection.

 You can deploy only one VPN gateway in each virtual network.

When you deploy a VPN gateway, you specify the VPN type: either **policy-based** or **route-based**. The main difference between these two types of VPNs is how traffic to be encrypted is specified. In Azure, both types of VPN gateways use a pre-shared key as the only method of authentication.

- **Policy-based VPN gateways** specify statically the IP address of packets that should be encrypted through each tunnel.  This type of device evaluates every data packet against those sets of IP addresses to choose the tunnel where that packet is going to be sent through.

- **In Route-based gateways**, `IPSec tunnels` are modeled as a network interface or virtual tunnel interface. IP routing (either static routes or dynamic routing protocols) decides which one of these tunnel interfaces to use when sending each packet. Route-based VPNs are the preferred connection method for on-premises devices. They're more resilient to topology changes such as the creation of new subnets.

Use a route-based VPN gateway if you need any of the following types of connectivity:

- Connections between virtual networks
- Point-to-site connections
- Multisite connections
- Coexistence with an Azure ExpressRoute gateway

If you’re configuring a VPN to keep your information safe, you also want to be sure that it’s a highly available and fault tolerant VPN configuration. There are a few ways to maximize the resiliency of your VPN gateway.
 - Active/StandBy
 - Active/Active
 - ExpressRoute failover
 - Zone Redundant gateways
  
### Azure DNS

Azure DNS is a hosting service for DNS domains that provides name resolution by using Microsoft Azure infrastructure.
Azure DNS can manage DNS records for your Azure services and provide DNS for your external resources as well. Azure DNS is integrated in the Azure portal and uses the same credentials, support contract, and billing as your other Azure services.
Azure DNS also supports **private DNS domains**. This feature allows you to use your own custom domain names in your private virtual networks, rather than being stuck with the Azure-provided names.

You can't use Azure DNS to buy a domain name. For an annual fee, you can buy a domain name by using App Service domains or a third-party domain name registrar. Once purchased, your domains can be hosted in Azure DNS for record management.

## Azure Data Migration

Azure supports both real-time migration of infrastructure, applications, and data using **Azure Migrate** as well as asynchronous migration of data using **Azure Data Box**.

### Azure Migrate

Azure Migrate is a service that helps you migrate from an on-premises environment to the cloud. Azure Migrate functions as a hub to help you manage the assessment and migration of your on-premises datacenter to Azure. It provides the following:
- U**nified migration platform**:  A single portal to start, run, and track your migration.
- **Range of tools**: A range of tools for assessment and migration.
- A**ssessment and migration**: In the Azure Migrate hub, you can assess and migrate your on-premises infrastructure to Azure.

### Azure Data Box

Azure Data Box is a physical migration service that helps transfer large amounts of data in a quick, inexpensive, and reliable way. The secure data transfer is accelerated by shipping you a proprietary Data Box storage device that has a maximum usable storage capacity of 80 terabytes. The Data Box is transported to and from your datacenter via a regional carrier. A rugged case protects and secures the Data Box from damage during transit.

## Azure file movement options

### AzCopy

AzCopy is a command-line utility that you can use to copy blobs or files to or from your storage account. With AzCopy, you can upload files, download files, copy files between storage accounts, and even synchronize files. AzCopy can even be configured to work with other cloud providers to help move files back and forth between clouds.

Synchronizing blobs or files with AzCopy is one-direction synchronization. When you synchronize, you designated the source and destination, and AzCopy will copy files or blobs in that direction. It doesn't synchronize bi-directionally based on timestamps or other metadata.

### Azure Storage Explorer

Azure Storage Explorer is a standalone app that provides a graphical interface to manage files and blobs in your Azure Storage Account. It works on Windows, macOS, and Linux operating systems and **uses AzCopy on the backend** to perform all of the file and blob management tasks. With Storage Explorer, you can upload to Azure, download from Azure, or move between storage accounts.

### Azure File Sync

Azure File Sync is a tool that lets you centralize your file shares in Azure Files and keep the flexibility, performance, and compatibility of a Windows file server. It’s almost like turning your Windows file server into a miniature content delivery network. Once you install Azure File Sync on your local Windows server, it will automatically stay bi-directionally synced with your files in Azure.


## Azure Directory Services

**Azure Active Directory (Azure AD)** is a directory service that enables you to **sign in** and access both Microsoft cloud applications and cloud applications that you develop. Azure AD can also help you maintain your **on-premises Active Directory** deployment.

For on-premises environments, **Active Directory** running on Windows Server provides an identity and access management service that's managed by your organization. **Azure AD** is Microsoft's cloud-based identity and access management service. With Azure AD, you control the identity accounts, but Microsoft ensures that the service is **available globally**.

**Azure AD** can detect sign-in attempts from unexpected locations or unknown devices.

Azure AD provides services such as:
- **Authentication**: This includes verifying identity to access applications and resources.
- **Single sign-on: Single sign-on (SSO)** enables you to remember only one username and one password to access multiple applications. A single identity is tied to a user, which simplifies the security model. As users change roles or leave an organization, access modifications are tied to that identity, which greatly reduces the effort needed to change or disable accounts.
- **Application management**: You can manage your cloud and on-premises apps by using Azure AD. Features like Application Proxy, SaaS apps, the My Apps portal, and single sign-on provide a better user experience.
- **Device management**: Along with accounts for individual people, Azure AD supports the registration of devices. Registration enables devices to be managed through tools like **Microsoft Intune**.

One method of connecting **Azure AD** with your **on-premises AD** is using **Azure AD Connect**. Azure AD Connect synchronizes user identities between on-premises Active Directory and Azure AD. Azure AD Connect synchronizes changes between both identity systems, so you can use features like SSO, multifactor authentication, and self-service password reset under both systems.

**Azure Active Directory Domain Services (Azure AD DS)** is a service that provides managed domain services such as domain join, group policy, lightweight directory access protocol (LDAP), and Kerberos/NTLM authentication. Just like Azure AD lets you use directory services without having to maintain the infrastructure supporting it, with Azure AD DS, you get the benefit of domain services without the need to deploy, manage, and patch domain controllers (DCs) in the cloud.
An Azure AD DS managed domain lets you run **legacy applications** in the cloud that can't use modern authentication methods.

### Azure Authentications Methods

Authentication is the process of establishing the identity of a person, service, or device. It requires the person, service, or device to provide some type of credential to prove who they are. 

Azure supports multiple authentication methods, including **standard passwords**, **single sign-on (SSO)**, **multifactor authentication (MFA)**, and **passwordless**.

**Single sign-on (SSO)** enables a user to sign in one time and use that credential to access multiple resources and applications from different providers. For SSO to work, the different applications and providers must trust the initial authenticator.
Single sign-on is only as **secure** as the initial authenticator because the subsequent connections are all based on the security of the **initial authenticator**.

**Multifactor authentication** is the process of prompting a user for an **extra form (or factor) of identification** during the sign-in process. MFA helps protect against a password compromise in situations where the password was compromised but the second factor wasn't.

Multifactor authentication provides additional security for your identities by **requiring two or more elements** to fully authenticate. These elements fall into three categories:

- **Something the user knows** – this might be a challenge question.
- **Something the user has** – this might be a code that's sent to the user's mobile phone.
- **Something the user is** – this is typically some sort of biometric property, such as a fingerprint or face scan.

**Passwordless authentication** methods are more convenient because the **password is removed and replaced with something you have, plus something you are, or something you know**.

Microsoft global Azure and Azure Government offer the following three **passwordless authentication** options that integrate with Azure Active Directory (Azure AD):
- **Windows Hello for Business** - Windows Hello for Business is ideal for information workers that have their own designated Windows PC. The biometric and PIN credentials are directly tied to the user's PC, which prevents access from anyone other than the owner. With public key infrastructure (PKI) integration and built-in support for single sign-on (SSO), Windows Hello for Business provides a convenient method for seamlessly accessing corporate resources on-premises and in the cloud.

- **Microsoft Authenticator app** - You can also allow your employee's phone to become a passwordless authentication method. You may already be using the Microsoft Authenticator App as a convenient multi-factor authentication option in addition to a password. You can also use the Authenticator App as a passwordless option.

- **FIDO2 security keys** - **The FIDO (Fast IDentity Online) Alliance** helps to promote open authentication standards and reduce the use of passwords as a form of authentication. FIDO2 is the latest standard that incorporates the web authentication (**WebAuthn**) standard.
Users can register and then select a FIDO2 security key at the sign-in interface as their main means of authentication. These **FIDO2 security keys are typically USB devices, but could also use Bluetooth or NFC**. With a hardware device that handles the authentication, the security of an account is increased as there's no password that could be exposed or guessed.

### Azure External Identities

An external identity is a person, device, service, etc. that is outside your organization. Azure AD External Identities refers to all the ways you can securely interact with users outside of your organization. 
If you're a developer creating consumer-facing apps, you can manage your customers' identity experiences.

External identities may sound similar to single sign-on. With **External Identities**, external users can "bring their own identities." Whether they have a corporate or government-issued digital identity, or an unmanaged social identity like Google or Facebook, they can **use their own credentials to sign in**. The **external user’s identity provider manages their identity**, and you manage access to your apps with **Azure AD or Azure AD B2C** to keep your resources protected.

The following capabilities make up External Identities:
- **Business to business (B2B) collaboration** - B2B collaboration users are represented in your directory, typically as guest users.
- **B2B direct connect** - Establish a mutual, two-way trust with another Azure AD organization.
- **Azure AD business to customer (B2C)** - Publish modern SaaS apps or custom-developed apps.

### Azure Conditional Access

Conditional Access is a **tool** that Azure Active Directory uses to **allow (or deny) access** to resources based on **identity signals**. These signals include **who the user is**, **where the user is**, and **what device** the user is requesting access from.

Conditional Access also provides a more **granular multifactor authentication** experience for users. For example, a user might not be challenged for second authentication factor if they're at a known location. However, they might be challenged for a second authentication factor if their sign-in signals are unusual or they're at an unexpected location.

During sign-in, Conditional Access collects signals from the user, makes decisions based on those signals, and then enforces that decision by allowing or denying the access request or challenging for a multifactor authentication response.

### Azure role-based access control (RBAC)

 The **principle of least privilege** says you should only grant access up to the level needed to complete a task.

Azure provides **built-in roles** that describe common access rules for cloud resources. You can also define your **own roles**. Each role has an associated **set of access permissions** that relate to that role. When you assign individuals or groups to one or more roles, they receive all the associated access permissions.

Role-based access control is **applied to a scope**, which is a **resource** or **set of resources** that this access applies to.

Scopes include:

- A management group (a collection of multiple subscriptions).
- A single subscription.
- A resource group.
- A single resource.

Azure **RBAC** is **hierarchical**, in that when you grant access at a parent scope, those **permissions are inherited** by all child scopes. 

Azure **RBAC** is **enforced on any action** that's initiated against an Azure resource that passes through **Azure Resource Manager**. Resource Manager is a management service that provides a way to organize and secure your cloud resources.

You typically access Resource Manager from the Azure portal, Azure Cloud Shell, Azure PowerShell, and the Azure CLI. Azure RBAC **doesn't** enforce access permissions at the application or data level. Application security must be handled by your application.

**Azure RBAC uses an allow model**. When you're assigned a role, Azure RBAC allows you to perform actions within the scope of that role. If one role assignment grants you read permissions to a resource group and a different role assignment grants you write permissions to the same resource group, you have both read and write permissions on that resource group.

### Zero Trust Model

Zero Trust is a security model that **assumes the worst case scenario** and protects resources with that expectation. Zero Trust assumes breach at the outset, and then verifies each request as though it originated from an uncontrolled network.

Zero Trust security model, which is based on these guiding principles:
- **Verify explicitly** - Always authenticate and authorize based on all available data points.
- **Use least privilege access** - Limit user access with Just-In-Time and Just-Enough-Access (JIT/JEA), risk-based adaptive policies, and data protection.
- **Assume breach** - Minimize blast radius and segment access. Verify end-to-end encryption. Use analytics to get visibility, drive threat detection, and improve defenses.

### Defense in Depth

A **defense-in-depth strategy** uses a series of mechanisms to slow the advance of an attack that aims at acquiring unauthorized access to data.

You can visualize **defense-in-depth as a set of layers**, with the data to be secured at the center and all the other layers functioning to protect that central data layer.
Each layer provides protection so that if one layer is breached, a subsequent layer is already in place to prevent further exposure. This approach removes reliance on any single layer of protection. It slows down an attack and **provides alert information** that security teams can act upon, either automatically or manually.

Here's a brief overview of the role of each layer:

- **The physical security layer** is the first line of defense to protect computing hardware in the datacenter.
- **The identity and access layer** controls access to infrastructure and change control.
- **The perimeter layer** uses distributed denial of service (DDoS) protection to filter large-scale attacks before they can cause a denial of service for users.
- **The network layer** limits communication between resources through segmentation and access controls.
- **The compute layer** secures access to virtual machines.
**The application layer** helps ensure that applications are secure and free of security vulnerabilities.
- **The data layer** controls access to business and customer data that you need to protect.

### Microsoft Defender for Cloud

Defender for Cloud is a monitoring tool for security posture management and threat protection. It monitors your cloud, on-premises, hybrid, and multicloud environments to provide guidance and notifications aimed at strengthening your **security posture**.

Defender for Cloud **provides the tools** needed to harden your resources, track your security posture, protect against cyber attacks, and streamline security management. Deployment of Defender for Cloud is easy, it’s already natively integrated to Azure.

Defender for Cloud helps you detect threats across:
- **Azure PaaS services** – Detect threats targeting Azure services including Azure App Service, Azure SQL, Azure Storage Account, and more data services. 
- **Azure data services** – Defender for Cloud includes capabilities that help you automatically classify your data in Azure SQL. 
- **Networks** – Defender for Cloud helps you limit exposure to brute force attacks. By reducing access to virtual machine ports, using the just-in-time VM access, you can harden your network by preventing unnecessary access. You can set secure access policies on selected ports, for only authorized users, allowed source IP address ranges or IP addresses, and for a limited amount of time.

### Assess, secure and defend

Defender for Cloud fills three vital needs as you manage the security of your resources and workloads in the cloud and on-premises:

**Continuously assess** – Know your security posture. Identify and track vulnerabilities.
**Secure** – Harden resources and services with Azure Security Benchmark.
**Defend** – Detect and resolve threats to resources, workloads, and services.

To help you understand how important each recommendation is to your overall **security posture**, Defender for Cloud groups the recommendations into **security controls** and adds a **secure score value** to each control. The secure score gives you an at-a-glance indicator of the **health of your security posture**, while the controls give you a working list of things to consider to improve your security score and your overall security posture.

When Defender for Cloud detects a threat in any area of your environment, it generates a security alert. Security alerts:
- Describe details of the affected resources
- Suggest remediation steps
- Provide, in some cases, an option to trigger a logic app in response


## Governance and Compliance

### Azure Blueprints

**Azure Blueprints** lets you **standardize** cloud subscription or environment deployments. Instead of having to configure features like Azure Policy for each new subscription, with Azure Blueprints you can define repeatable settings and policies that are applied as new subscriptions are created. 

Each **component** in the blueprint definition is known as an **artifact**.

It is possible for artifacts to have no additional parameters (configurations). Artifacts can also contain one or more parameters that you can configure. You can specify a parameter's value when you create the blueprint definition or when you assign the blueprint definition to a scope. In this way, you can maintain one standard blueprint but have the flexibility to specify the relevant configuration parameters at each scope where the definition is assigned.

Azure Blueprints deploy a new environment based on all of the requirements, settings, and configurations of the associated artifacts. Artifacts can include things such as:
- Role assignments
- Policy assignments
- Azure Resource Manager templates
- Resource groups

Azure Blueprints are **version-able**, allowing you to create an initial configuration and then make updates later on and assign a new version to the update. 

## Azure Policy

Azure Policy is a service in Azure that enables you to create, assign, and manage policies that **control or audit your resources**. These policies enforce different rules across your resource configurations so that those configurations stay compliant with corporate standards.

Azure Policy evaluates your resources and **highlights** resources that **aren't compliant** with the policies you've created. Azure Policy can also **prevent** noncompliant resources from being created.

Azure Policies are **inherited**, so if you set a policy at a high level, it will automatically be applied to all of the groupings that fall within the parent. 

Azure Policy comes with built-in policy and initiative definitions for Storage, Networking, Compute, Security Center, and Monitoring.  Azure Policy also evaluates and monitors all current VMs in your environment, including VMs that were created **before the policy was created**.

An **Azure Policy initiative** is a way of grouping related policies together. The **initiative** definition contains all of the policy definitions to help track your compliance state for a larger goal.

### Resource Locks

A resource lock prevents resources from being **accidentally deleted or changed**.

Resource locks can be applied to **individual resources, resource groups, or even an entire subscription**. Resource locks are **inherited**, meaning that if you place a resource lock on a resource group, all of the resources within the resource group will also have the resource lock applied.

There are two types of resource locks:
- **Delete** means authorized users can still read and modify a resource, but they can't delete the resource.
- **ReadOnly** means authorized users can read a resource, but they can't delete or update the resource. Applying this lock is similar to restricting all authorized users to the permissions granted by the **Reader role**.

Although locking helps prevent accidental changes, you can still make changes by following a **two-step process**.
To modify a locked resource, **you must first remove the lock**. After you remove the lock, you can apply any action you have permissions to perform. Resource locks apply regardless of RBAC permissions. Even if you're an owner of the resource, you must still remove the lock before you can perform the blocked activity.

### Service Trust Portal

The Microsoft Service Trust Portal is a portal that provides access to various content, tools, and other resources about Microsoft security, privacy, and compliance practices.

## Cost Management in Azure

Azure shifts development costs from the **capital expense (CapEx)** of building out and maintaining infrastructure and facilities to an **operational expense (OpEx)** of renting infrastructure as you need it, whether it’s compute, storage, networking, and so on.

That** OpEx cost** can be impacted by many **factors**. Some of the impacting factors are:
- Resource type
- Consumption
- Maintenance
- Geography
- Subscription type
- Azure Marketplace

When you provision an Azure resource, Azure creates **metered instances** for that resource. The meters track the resources' usage and generate a usage record that is used to calculate your bill.

The **pricing calculator** and the total **cost of ownership (TCO) calculator** are two calculators that help you understand potential Azure expenses. 
The **pricing calculator** is designed to give you an estimated cost for provisioning resources in Azure. 
The **TCO calculator** is designed to help you compare the costs for running an on-premises infrastructure compared to an Azure Cloud infrastructure. With the TCO calculator, you enter your current infrastructure configuration, including servers, databases, storage, and outbound network traffic. The TCO calculator then compares the anticipated costs for your current environment with an Azure environment supporting the same infrastructure requirements.

**Cost Management** provides the ability to quickly check Azure resource costs, create **alerts** based on resource spend, and **create budgets** that can be used to automate management of resources.
You use **cost analysis** to explore and analyze your organizational costs. You can view aggregated costs by organization to understand where costs are accrued and to identify spending trends. And you can see accumulated costs over time to estimate monthly, quarterly, or even yearly cost trends against a budget.

## Tools for managing and deploying resources

To get the most out of Azure, you need a way to interact with the Azure environment, the management groups, subscriptions, resource groups, resources, and so on. Azure provides multiple tools for managing your environment, including the:

- **Azure portal** - is a web-based, unified console that provides an alternative to command-line tools. With the Azure portal, you can manage your Azure subscription by using a graphical user interface.
- **Azure Cloud Shell** - is a browser-based shell tool that allows you to create, configure, and manage Azure resources using a shell. Azure Cloud Shell support both **Azure PowerShell** and the **Azure Command Line Interface (CLI)**, which is a Bash shell.


### Azure PowerShell

Azure PowerShell is a shell with which developers, DevOps, and IT professionals can run commands called **command-lets (cmdlets)**. These commands call the **Azure REST API** to perform management tasks in Azure. Cmdlets can be run independently to handle one-off changes, or they may be combined to help orchestrate complex actions.

In addition to be available via Azure Cloud Shell, you can install and configure Azure PowerShell on Windows, Linux, and Mac platforms.

### Azure Command Line Interface (CLI)

The Azure CLI is functionally equivalent to Azure PowerShell, with the primary difference being the syntax of commands. While Azure PowerShell uses PowerShell commands, the **Azure CLI uses Bash commands**.

### Azure Arc

In utilizing Azure Resource Manager (ARM), **Arc** lets you extend your Azure compliance and monitoring to your **hybrid and multi-cloud configurations**. Azure Arc simplifies governance and management by delivering a consistent multi-cloud and on-premises management platform.

Currently, Azure Arc allows you to manage the following resource types hosted outside of Azure:

- Servers
- Kubernetes clusters
- Azure data services
- SQL Server
- Virtual machines (preview)

### ARM - Azure Resource Manager & ARM Templates

Azure Resource Manager (ARM) is the **deployment and management service for Azure**. It provides a management layer that enables you to create, update, and delete resources in your Azure account. Anytime you do anything with your Azure resources, ARM is involved.

When a user sends a request from any of the Azure tools, APIs, or SDKs, ARM receives the request. ARM authenticates and authorizes the request. Then, ARM sends the request to the Azure service, which takes the requested action. You see consistent results and capabilities in all the different tools because all requests are handled through the same API.

With Azure Resource Manager, you can:

- Manage your infrastructure through **declarative templates** rather than scripts. A **Resource Manager template is a JSON file** that defines what you want to deploy to Azure.
- Deploy, manage, and monitor all the resources for **your solution as a group**, rather than handling these resources individually.
- **Re-deploy** your solution throughout the development life-cycle and have confidence your resources are deployed in a consistent state.
- Define the **dependencies between resources**, so they're deployed in the correct order.
- **Apply access control** to all services because RBAC is natively integrated into the management platform.
- **Apply tags** to resources to logically organize all the resources in your subscription.
- Clarify your organization's **billing** by viewing costs for a group of resources that share the same tag.


**Infrastructure as code** is a concept where you manage your infrastructure as lines of code. Leveraging Azure Cloud Shell, Azure PowerShell, or the Azure CLI are some examples of using code to deploy cloud infrastructure. **ARM templates** are another example of infrastructure as code at work.

By using **ARM templates**, you can describe the resources you want to use in a **declarative JSON format**. With an ARM template, the deployment code is **verified before any code is run**. This ensures that the resources will be created and connected correctly. The template then orchestrates the **creation of those resources in parallel**. That is, if you need 50 instances of the same resource, all 50 instances are created at the same time. You deploy the template through **one command**, rather than through multiple imperative commands.

With **deployment scripts**, you can add PowerShell or Bash scripts to your templates. The deployment scripts extend your ability to set up resources during deployment. A script can be included in the template or stored in an external source and referenced in the template. Deployment scripts give you the ability to complete your end-to-end environment setup in a single ARM template.

## Azure Monitoring Tools

### Azure Advisor

**Azure Advisor** **evaluates** your Azure resources and **makes recommendations** to help improve reliability, security, and performance, achieve operational excellence, and reduce costs. Azure Advisor is designed to help you save time on cloud optimization. The recommendation service includes **suggested actions** you can take right away, postpone, or dismiss.

### Azure Health Service

Azure Service Health helps you **keep track** of Azure resource, both your specifically deployed resources and the **overall status of Azure**. Azure service health does this by combining three different Azure services:
- **Azure Status** is a broad picture of the status of Azure globally. Azure status informs you of service outages in Azure on the Azure Status page. The page is a global view of the health of all Azure services across all Azure regions.
- **Service Health** provides a narrower view of Azure services and regions. It focuses on the Azure services and regions you're using. This is the best place to look for service impacting communications about outages, planned maintenance activities, and other health advisories because the authenticated Service Health experience knows which services and resources you currently use. 
- **Resource Health** is a tailored view of **your** actual Azure **resources**. It provides information about the health of your individual cloud resources, such as a specific virtual machine instance. Using Azure Monitor, you can also **configure alerts** to notify you of availability changes to your cloud resources.

###  Azure Monitor

**Azure Monitor** is a platform for **collecting** data on your resources, **analyzing** that data, **visualizing** the information, and even **acting** on the results. Azure Monitor can monitor Azure resources, your on-premises resources, and even multi-cloud resources like virtual machines hosted with a different cloud provider.

**Azure Log Analytics** - is the tool in the Azure portal where you’ll write and run **log queries** on the data gathered by Azure Monitor. Log Analytics is a robust tool that supports both simple, complex queries, and data analysis. 

**Azure Monitor Alerts** are an automated way to stay informed when Azure Monitor detects a threshold being crossed. You set the **alert conditions**, the notification actions, and then Azure Monitor Alerts notifies when an alert is triggered. Depending on your configuration, Azure Monitor Alerts can also **attempt corrective action**.

**Application Insights**, an Azure Monitor feature, **monitors your web applications**. Application Insights is capable of monitoring applications that are running in Azure, on-premises, or in a different cloud environment.
There are two ways to configure Application Insights to help monitor your application. You can either install an **SDK in your application**, or you can use the **Application Insights agent**. The Application Insights agent is supported in C#.NET, VB.NET, Java, JavaScript, Node.js, and Python.
Not only does Application Insights help you monitor the performance of your application, but you can also configure it to **periodically send synthetic requests to your application**, allowing you to check the status and monitor your application even during periods of low activity.



## Additional Azure Services

- **App Services** - Web Apps, Mobile Apps, API Apps, Logic Apps, ...
- **Azure Container Services** - Azure Container Instances, Azure Kubernetes Service, Azure Service Fabric, ...
- **Windows Virtual Desktop (WVD)** - is a **desktop and app virtualization** **service** that **runs** **on** **Azure**. It **provides** **Windows** **10** **virtual desktops** and applications on-demand or **on-premises**.
- **Data Services** - Azure SQL Database, Azure Cosmos DB, Azure Data Lake Storage, Azure HDInsight, Azure Data Factory, Azure Stream Analytics, Azure Machine Learning, Azure Search, Azure IoT Hub, Azure Databricks, Azure Synapse Analytics, ...

## Azure Internet of Things (IoT)
- IoT Hub
- IoT Central
- Azure Sphere
  
## Big data an analytics
- Azure HDInsight
- Azure Databricks
- Azure Synapse Analytics

## Artificial Intelligence (AI) and Machine Learning (ML)
- Azure Machine Learning
- Cognitive Services
- Bot Service
  

## Application Development

- Azure DevOps
- GitHub
- GitHub actions for Azure
- DevTest Labs
