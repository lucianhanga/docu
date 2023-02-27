# Concepts, Services & Solutions

## Cloud Computing

Cloud Computing based on **virtualization technology**, which allows users to access **computing resources**, **storage**, and **applications** over the Internet.

They have the following characteristics:
- **On-demand self-service**: Users can **provision computing resources** as needed without requiring human interaction with each service provider.
- **Broad network access**: Users can access resources and applications from almost any device connected to the Internet.
- **Resource pooling**: The provider's computing resources are pooled to serve multiple customers using a **multi-tenant model**, with different physical and virtual resources dynamically assigned and reassigned according to customer demand.


### Benefits of Cloud Computing

- **Scalability**: The ability to **increase** computing resources **dynamically** as needed.
- **Elasticity**:  The ability to **grow or shrink** capacity as **demand changes**.
- **Disaster recovery**: The ability to **recover quickly** from **disasters**. **Replication** of data and applications to a **secondary site** in a **different region** is a common approach to disaster recovery.
- **High availability and fault tolerance**: The ability to **provide continuous** service to users **without interruption**. **Redundancy** is a common approach to high availability and fault tolerance.
- **Agility**: The ability to **quickly** and **efficiently** **respond** to **business needs**. Agility is achieved through **automation** and **self-service** capabilities.
- **Predictable costs**: The ability to **predict** the **costs** of using cloud resources. **Metering** and **billing** are used to provide transparency into the costs of using cloud resources.
  
### CapEx vs. OpEx

**CapEx: Capital Expenditure** - **upfront costs** for **hardware** and **software**. Typical for **on-premises** solutions.
  - pay upfront versus paying monthly.
  - pay for a bigger capacity than you need for the cases when you need more capacity.

**OpEx: Operational Expenditure** - **ongoing costs** for **hardware** and **software**. Typical for **cloud** solutions.
 - pay as you go (PAYG) : **pay for what you use** and **only when you use it**.
 - pay monthly versus paying upfront.
  
Pay as you go (PAYG) is a consumption-based pricing model that allows you to pay for the resources you use as you use them. This model is also known as **pay for what you use** and **only when you use it**.

## Cloud Computing Models

There are three main cloud computing models. The key difference between them is the **location** of the **resources** and **applications**.

### Public Cloud

Public cloud is a **shared** cloud computing environment that is **open** to the **public**. It is **managed** by a **third-party provider**.
-  owned by the cloud service provider.
-  multi-tenant model.
-  accessible over the Internet or over VPN connections.

### Private Cloud

Private cloud is a **dedicated** cloud computing environment that is **managed** by an **organization** for its **own use**. Usually, it is **located** on **premises**. Most of the tine is **missing the ability** to dynamically scale resources and automatically provision new resources.

### Hybrid Cloud

Hybrid cloud is a **combination** of **public** and **private** clouds that **remain unique entities** but are **bound** together by **standardized** or **proprietary** technology that enables data and application portability.


## Cloud Services

Cloud services are **offered** by **cloud providers** to **users** over the Internet. They are **bundled** into **cloud service models**. Cloud services are a shared responsibility model - the cloud provider is responsible for the **infrastructure** and the **user** is responsible for the **applications**.

### Infrastructure as a Service (IaaS)

Infrastructure as a Service (IaaS) is a **cloud service model** that provides **virtualized computing resources** over the Internet. Users can provision virtual machines, storage, and networking resources on demand.

Azure natively provides the following IaaS services:
- **Virtual Machines** 
- **Virtual Networks**
- **Storage**
- Transfer existing on-premises servers to Azure using **Azure Migrate** or **P2V** migration.
- Take advantage of high availability options and cost saving using pay-as-you-go subscriptions.

### Platform as a Service (PaaS)

Platform as a Service (PaaS) is a **cloud service model** that provides **virtualized computing resources** and a **runtime environment** for **developing**, **testing**, and **deploying** applications. Users can provision virtual machines, storage, and networking resources on demand. 

Benefits of PaaS:
- don't worry about the underlying infrastructure.
- simply focus on the application development.
- 

### Software as a Service (SaaS)

Software as a Service (SaaS) is a **cloud service model** that provides **software applications** to users over the Internet. Users can access the applications from almost any device connected to the Internet. 

Benefits of SaaS:
- don't worry about the underlying infrastructure.
- provide easy access to applications such as **Microsoft Office 365**.











