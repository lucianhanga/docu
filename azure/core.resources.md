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

## Networking Resources

**Networking resources** are those resources on-demand that provide networking capabilities.

The most common example of **Networking resources** are **Virtual Networks**.

- **Virtual Networks (vNet)** are used to connect Azure resources to **each other**, to **on-premises** resources, and over the Internet. They provide a secure network connection between **resources**.

- **VPN Gateway** is used to connect **on-premises** **networks** to **Azure** **virtual networks** over **Site-to-Site** **VPN** connections.
S2S - Site-to-Site VPN
P2S - Point-to-Site VPN

- **ExpressRoute** is used to create **private** connections between **Azure** and **on-premises** **networks**.


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
