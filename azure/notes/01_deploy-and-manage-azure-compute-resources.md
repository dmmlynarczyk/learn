# Deploy and Manage Azure Compute Resources

20%-25% of AZ-104 exam.  

- [Deploy and Manage Azure Compute Resources](#deploy-and-manage-azure-compute-resources)
  - [Creating A Virtual Machine](#creating-a-virtual-machine)
    - [Availability Options](#availability-options)
    - [Security Types](#security-types)
    - [Spot Instances](#spot-instances)
    - [Sizes](#sizes)
    - [Hibernation](#hibernation)
    - [Disks](#disks)
    - [Networking](#networking)
    - [Management and Advanced Options](#management-and-advanced-options)
  - [Azure Backup](#azure-backup)
  - [Resizing VMs](#resizing-vms)
  - [Adding Additional Data Disks](#adding-additional-data-disks)
  - [Azure Bastion Service](#azure-bastion-service)
  - [Virtual Machine Scale Sets](#virtual-machine-scale-sets)
    - [Virtual Machine Scaling](#virtual-machine-scaling)
  - [Automate Deployment of Resources By Using Templates](#automate-deployment-of-resources-by-using-templates)
  - [Azure Bicep Files](#azure-bicep-files)
  - [Azure App Services](#azure-app-services)
    - [Deployment](#deployment)
    - [Web App Settings](#web-app-settings)
    - [Scaling](#scaling)
  - [Containers](#containers)
    - [Azure Container Instances](#azure-container-instances)
    - [Azure Container Apps](#azure-container-apps)
  - [Additional Quick Notes](#additional-quick-notes)


## Creating A Virtual Machine

An Azure Virtual Machine (VM) is on of several types of on-demand, scalable compute resources that Azure offers.  It gives you the flexibility of virtualization without having to buy and maintain physical hardware.  However you will still need to perform basic maintenance tasks such as configuring, patching, and installing software on the VMs.

### Availability Options

There are four availability options you can choose from when creating your machine:
- **No infrastructure redundancy required**: self explanatory.
  - Great if it is a stand-alone VM since data is not being passed between VMs.
- **Availability zone**: Physically separate your resources within an Azure region.
  - Used to protect applications against Azure data center failures.  Since AZs are physically separate data centers within an Azure region, each with independent power, cooling, and networking. *This protects applications and data from datacenter-level failures.*
  - Deploying VMs across at least three Availability Zones in a region is a fundamental requirement for the 99.99% SLA.
- **Virtual machine scale set**: Distribute VMs across zones and fault domains at scale.
- **Availability set**: a logical grouping of VMs within a data center that ensures they are distributed across multiple fault domains (power/network) and update domains (separate maintenance windows) to maximize uptime.
  - The purpose if to protect against hardware failures and planned maintenance outages by ensuring that all of your VMs *DO NOT* go down at the same time.
  - ***99.95% SLA*** *when you have two or more VMs in the set.*
  - Two failures are:
    - **Fault domains**: something relating to the computer failed.
      - Virtual machines in the same fault domain share a common power source and physical network switch.
    - **Update Domains**: planned maintenance from Microsoft updating hardware/infrastructure.
      - Virtual machines in the same update domain will be restarted together during planned maintenance.
      - Azure never restarts more than one update domain at a time.

### Security Types

**Security Type**: refers to the different security features available for a virtual machine. There are three options:
- **Standard**: The basic level of security for your virtual machines.
- **Trusted launch virtual machines**: protects against persistent and advanced attacks on Gen 2 virtual machines with configurable features like secure boot and virtual Trusted Platform Module (vTPM).
- **Confidential virtual machines**: on top of Trusted launch, Confidential virtual machine offers higher *confidentiality and integrity guaranteed* with hardware-based trusted execution environment.

### Spot Instances

**Spot instances**: are a way to save money, you do not have to pay full price, but as soon as someone comes along willing to pay full price, you will lose your instance.  
These are great for low-priority workloads.

### Sizes

**Instance Family**:
- **General Purpose**: balanced VM.
  - Balanced CPU-to-memory ratio.
  - Ideal for testing and development, small to medium databases, and low to medium traffic web servers.
- **Compute Optimized**: double the CPU cores.
  - High CPU-to-memory ratio.
  - Good for medium traffic web servers, network appliances, batch processes, and application servers.
- **Memory Optimized**: double the memory.
  - High memory-to-core ratio.
  - Great for relational database servers, medium to large caches, and in-memory analytics.
- **Storage Optimized**: double the local storage.
  - High disk throughput and IO.
  - Ideal for Big Data, SQL, and NoSQL databases.
- **GPU**: access to a graphics processing unit.
  - Specialized virtual machines targeted for heavy graphic rendering and video editing available with single or multiple GPUs.
- **High-Performance Compute**: fastest everything.
  - Fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).

### Hibernation

**Hibernation**: saves you time and money by deallocating your virtual machine and saving the contents of its RAM to the root volume.  
This allows you to resume from where you left off when your VM restarts.  

### Disks

- Virtual machines come with one OS disk and one temporary disk (for short term storage).  
  - Additional data disks can be attached.  
- Azure disk storage encryption automatically encrypts data at rest by default, but you can also encrypt at host if you want.
- **Locally redundant storage (data is replicated within a single datacenter) disk types**
  - **Premium SSD**: Best for production and performance sensitive workloads.
  - **Standard SSD**: Best for web servers, lightly used enterprise applications and dev/test.
  - **Standard HDD**: Best for backup, non-critical, and infrequent access.
- **Zone-redundant storage (data is replicated to three zones)**
  - **Premium SSD**: Best for production workloads that need storage resiliency against zone failures.
  - **Standard SSD**: Best for web servers, lightly used enterprise applications and dev/test that need storage resiliency against zone failures.
- **Managed Disks**: are highly available by design.  For single-instance VMs using Managed Disks, Azure guaranteed 99.9% SLA.
  - More importantly, for VMs deployed in Availability Zones, Managed Disks automatically replicate their data to multiple storage stamps within the chosen zone.
  - Using Managed Disks with Availability Zones is key to the 99.9% SLA for VMs.
  - Provide the capability to increase the size of an attached data disk while the virtual machine is still running.  All you will need to do is extend the partition to utilize the new space.

### Networking

One of the more important aspects when creating a virtual machine.  
Every virtual machine must be attached to a virtual network.  
You can either create a new one or attach it to a pre-existing virtual network.  
Similar to OS disk you have the option of deleting the public IP and NIC when the VM is deleted.  
**Accelerated networking**: enables low latency and high throughput on the network interface.  

### Management and Advanced Options

- If your VM needs to access other resources and you want to use RBAC and Entra ID to manage those permissions, you can create a system assigned managed identity.  
- A relatively new options is you can now login with Entra ID.  
- **Auto-shutdown**: allows you to select a time to automatically shut down your machine.  
- **Enable recommended alert rules**: You can enable the 7 most recommended alerts to get notified on important events happening on your resource.  
- **OS Guest Diagnostics**: give you metrics every minute for your virtual machine.  You can use them to create alerts and stay informed on your applications.  
- **Extensions**: allows you to add new features, like configuration management or antivirus protection, to your virtual machine using extensions.  
- **Azure Dedicated Hosts**: allows you to provision and manage a physical server within our data centers that are dedicated to your Azure subscription.  
  - Gives you assurance that only VMs from your subscription are on the host. 

## Azure Backup

- **Azure Backup**: protects your VMs and their data through the Recovery Services vaults that store backup copies with configurable retention policies.
  - **Backups must be in the same region as the VM**
  - You can restore entire VMs or individual files
  - Provides automated scheduling with point-in-time recovery to meet your RPO/RTO requirements.
  - Essential for ensuring computer workloads have proper data protections and can be quickly restored after failures or disasters. 
  - Azure Backup only takes snapshots of the VM disks, meaning that **even if the VM status is running or stopped, you can still create a backup** as long as the disk is attached to the VM.

## Resizing VMs

A huge benefit of cloud based virtual machines is the easy ability to resize them.  
From your VM page, on the blade select Size under the "Availability + scale" section.  
**This is a disruptive event** by changing the size the VM will have to be restarted.  

## Adding Additional Data Disks

- More often than not, we will need to store data on the virtual machines, but since data should not be stored on the C: drive, and the D: drive is ephemeral we will need to add data disks. *This is the recommended way.*
  - Data on the D: drive is ephemeral means that data stored on that drive is temporary and will be lost if the VM is stopped/deallocated, resized, or moved to different physical hardware. So *never store important data there that you cannot afford to lose.*
- First we will need to shutdown our VM.
- Under blade category "Settings" > "Disks"
  - Here you can create a new data disk to add.
  - After your new drive is created and added you will need to mount it in the OS. Just need to go to Disk management, and format a new simple volume!  

## Azure Bastion Service

RDP should be removed as it is very insecure and not a good option long term. If you do choose to use it, it is best to change source to only specific IPs.  But a safer alternative is **Azure Bastion Service**.
**Bastion**: is a way to connect remotely to your VM through the Azure portal. No public IPs required, and port 3389 and 22 do not need to be opened anymore.
- There are several tiers in Bastion:
  - Developer
  - Basic
  - Standard
  - Premium

## Virtual Machine Scale Sets

Instead of scaling *up* (larger CPU, more RAM, etc.) we also have the option to scale *out* (more of the same device).  And that has to deal with increasing the number of identical load balanced instances there are.  
This helps in reducing the risk of the possibility of your application going down, now there are two, four, eight or however many instances running your application making it much more fault tolerant and highly available.  
**Virtual Machine Scale Set (VMSS)**: is a group of identical, load balanced VMs that can automatically scale in or scale out.  Designed for stateless servers like web applications and web servers, where it does not need to remember anything about previous interactions.  
- Auto scaling
- Redundancy
- Load balancing

- **Orchestration modes**: determines how VMs are handled by the scale set.  
  - Orchestration mode is defined when you create the scale set and cannot be changed or updated later.
  - There are two options:  
    - **Flexible**: achieve high availability at scale with identical or multiple virtual machine types.  More complicated and can handle stateful instances.  
    - **Uniform**: optimized for large scale stateless workloads. You cannot manage any single machine as it is all the exact same.

**Overprovisioning**: When turned on the scale set will spin up more VMs than you asked for, and will delete the extra VMs once the requested number of VMs are successfully provisioned.  It improves success rates and reduces deployment times. *You are not billed for the extra VMs and they do not count toward your quota limits.*

**Health Monitoring**: Azure will check VMs health and see that things are responding properly.  If it detects health issues it will begin the process of provisioning new VMs and also taking off connections to the failing machine.

[More about Virtual Machine Scale Sets](https://learn.microsoft.com/en-us/azure/virtual-machine-scale-sets/overview)

### Virtual Machine Scaling

**Manual Scaling**:
- On the blade menu in the VMSS service page, there is "Availability + scale" > "Scaling".  
- In here you are able to manually override the number of instance you can create up to 1000 instances.  
- This is not the preferred method, as automatic is better management wise, *BUT* for predictable workloads, manual scaling is perfectly fine.  
  - If you know you always need 5 instances, etc it is perfect. 

*Manual scaling is an important way that you can save money if you are good about understanding and managing your needs and resources.*

**Automatic Scaling**:
- Allows you to scale on any schedule, based on any metrics or predictively.
- **Predictive Autoscale**: uses machine learning to forecast when your machine might need more capacity.
  - It knows that every Monday at 10AM there is a spike in traffic so it might provision a new instance at 9:45AM to be ready for that spike at 10AM and once the spike is done, it will scale back down.

## Automate Deployment of Resources By Using Templates

**Azure Resource Manager (ARM)**: is the centralized deployment model. When you run deployment commands they flow through ARM which then interacts with Azure Resources behind the scenes.  
- The ARM model runs on JSON templates.
- The four elements of an ARM template are:
  - **Parameters**: variables that can be passed into the template.
    - Input values that you provide when deploying the template to customize the deployment (like VM size, location, or admin username).
  - **Variables**: variables that are NOT passed into the template (like a parameter) but are instead created and used inside of the template
    - Internal values calculated or defined within the template to simplify expressions and avoid repetition throughout the template.
  - **Resources**: are the list of actual resources that will be created or configured by the template
  - **Outputs**: values that the template returns after deployment completes, such as IP addresses or connection strings that you might need for other deployments or applications.  
[The official Microsoft Azure GitHub repository](https://github.com/Azure/azure-quickstart-templates) contains sample ARM templates for almost every service in Azure.

## Azure Bicep Files

**What is Bicep?**  
Bicep is a domain-specific language (DSL) that simplifies writing Azure Resource Manager templates by using a cleaner, more readable syntax instead of complex JSON. It compiles down to standard ARM templates but is much easier to write and maintain, making Infrastructure as Code more accessible for Azure deployments.  

Bicep has an extension in VSCode found [here.](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-bicep)  This allows you to edit bicep files with intellisense and other useful features in VSCode.  

## Azure App Services

**Azure App Service**: is a Platform-as-a-Service (PaaS) offering that lets you deploy and host web applications, APIs, and mobile backends without managing the underlying servers or infrastructure. You just upload your code (in languages like .NET, Java, Python, Node.js, PHP) and Azure handles the scaling, patching, and maintenance automatically.
- Some runtime stacks will only work on Windows such as ASP.NET, while Ruby will only work with Linux.  Common runtime stacks include:
  - ASP.NET V4.8 = **Windows**
  - Node 16 LTS = **Windows & Linux**
  - PHP 8.2 = **Linux**
  - Python 3.10 = **Linux**
  - Java 11 = **Windows & Linux**
- Depending on your App Service Plan you may not be able to add a staging slot for your application.  If this happens you can upgrade your App Service plan to a Standard or Premium tier.

**Zone Redundancy**: an App Service can be deployed as a zone redundant service in the regions that support it.  This is a deployment time only decision.  *You cannot make an App Service plan zone redundant after it has been deployed.*  You must have a premium pricing plan selected in order to be able to utilize zone redundancy.  

### Deployment

**Continuous Deployment**: can be setup to easily deploy code from your GitHub repository via GitHub Actions.

**GitHub Settings**: can be setup to push content to your app whenever there are code changes made to your repository. This is a type of CI/CD in Azure.
Other options for CI/CD are:
- Bitbucket
- Local Git
- Azure Repos

### Web App Settings

**Application Settings**: allow you to separate out the dynamic variables of an application from the code.  You don't want important settings buried in the code.  Found in the **Environment variables** blade.  

### Scaling

Just like VMSS you have the ability to scale up/down, and in/out.

For in/out scaling you also have the option to either scale automatically or manually.  
You can turn *Session Affinity* on to ensure an end user always gets the same web app server.  

## Containers

**Container**: is a lightweight, portable package that includes an application and everything it needs to run (code, runtime, libraries, settings, etc).
- Think of it as a standardized shipping container that can run consistently anywhere, whether on your laptop, Azure, or any other cloud platform.
- Azure Container Instances and Azure Container Apps are services that run these containers without you needing to manage the underlying servers.
- Kubernetes is the industry standard for containers, but not a requirement in AZ104.
- **Azure Container Groups**: a collection of containers running in the same host.
- **Azure Container Registry**: a private container that lives in Azure that you can store your private container images.

### Azure Container Instances

- **Azure Container Instances**: used to create and manage Docker containers in Azure without having to set up virtual machines or manage additional infrastructure.
  - Single node instances instead of clusters like in Kubernetes.

### Azure Container Apps

- **Azure Container Apps**: provide the flexibility of web apps and the simplicity of Kubernetes.
  - It automatically handles scaling, load balancing, and networking.
  - Ideal for microservices, APIs, and event-driven applications that need to scale up and down based on demand.
  - Serverless containers!

## Additional Quick Notes

- To guarantee an application uptime SLA of 99.99% at the infrastructure level:
  - Deploy the virtual machine across multiple Availability Zones within the selected Azure Region
  - Place the virtual machines behind an Azure Standard Load Balancer
  - Implement managed disks for all virtual machines