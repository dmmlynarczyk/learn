# Implement and Manage Virtual Networking

15%-20% of AZ-104 exam.  

- [Implement and Manage Virtual Networking](#implement-and-manage-virtual-networking)
  - [Virtual Networks](#virtual-networks)
    - [Security Settings](#security-settings)
    - [Public IP Address](#public-ip-address)
  - [VNet Peering](#vnet-peering)
    - [Global Peering](#global-peering)
    - [Virtual Network Gateway](#virtual-network-gateway)
  - [Site-to-Site VPN](#site-to-site-vpn)
  - [Azure DNS](#azure-dns)
  - [Security Groups](#security-groups)
  - [Load Balancers](#load-balancers)
  - [Network Watcher](#network-watcher)


## Virtual Networks

**Virtual Networks**: are your private network space in the cloud that logically isolates your Azure resources from other customers.  They work like a traditional network in your office - you can control IP addresses, create and modify subnets, set up security rules, and connect to other network or the internet, giving you secure communication between your Azure resources.  
Virtual Networks enable many types of Azure resources, such as VMs, to securely communicate with each other, the internet, and on-premises networks.

### Security Settings

- **Virtual Network Encryption**: to encrypt traffic traveling within the virtual network.
  - Traffic to public IP addresses is not encrypted.
  - Your VMs must have accelerated networking enabled.
- **Azure Bastion**: *PAID SERVICE* that provides secure RDP/SSH connectivity to your virtual machines over TLS.
  - When you connect via Bastion your VMs do not need a public IP address.
  - Provides secure RDP and SSH connectivity to all of the VMs in the virtual network in which it is provisioned.
  - Protects your networks from exposing RDP/SSH ports to the outside world while still providing secure access using RDP/SSH.
- **Azure Firewall**: is a managed cloud-based network security service that protects your Azure Virtual Network resources.
- **DDoS Network Protection**: *PAID SERVICE* that offers DDoS mitigation capabilities.

### Public IP Address

> [!NOTE]
> Public IP addresses are not free, important to remember this.

Basic tier of public IP addresses has been deprecated in Azure, now only have the option for Standard tier.  *NO DYNAMIC IP ADDRESSES ONLY STATIC NOW.*  

- **DDoS Protection**: helps to defend against DDoS attacks directed at your resources.  There are three options:
  - **Network**: inherits DDoS protection from virtual network
  - **IP**: specific to this public IP only
  - **Disabled**: no protection needed/wanted

- To associate your new public IP address with a device you need to select the 'Associate' link on the public IP.  Or you can go to the network interface card on your device, and associate the public IP in there.  

## VNet Peering

- By default any server running on a virtual network will not be able to communicate with a server on a different virtual network.  They will be able to talk to servers on the same virtual network though.
- **Peering**: is the idea of setting up a relationship on two different virtual networks that they recognize each other.  Allowing virtual machines running on one VNet will be able to communicate with virtual machines on another VNet.
> [!IMPORTANT]
> The IPs defined in one virtual network have to be non-overlapping.

- VNets can have peerings with multiple other VNets.  Think hub and spoke topology.
- **Traffic to remote virtual network**: this will need to be allowed if you wish to allow communication between the two virtual networks.
  - This option allows the remote virtual network address space to be included as part of the Virtual_Network tag.
- **Traffic forwarded from remote virtual network**: this setting allows forwarded traffic from remote virtual network (traffic not originating from inside remote virtual network) into NewTest1. 
  - This allows a hub and spoke topology to actually forward non-peered network together.
- If you know the Resource ID of two different resources in different subscriptions you can peer them together also!
- If your VNet peering connection is in a **Disconnected** state, it means one of the links created was deleted.  To re-establish a peering connection, you will need to delete the disconnected peer and recreate it.

### Global Peering

> [!NOTE]
> Both ingress and egress traffic is charged at both ends of the peered networks.

- **Global Peering**: connects two Azure virtual networks that reside in **different Azure regions** (or subscriptions) so they can communicate privately over Microsoft's backbone network.  
  - Once peered, resources in either VNet can reach each other using their private IP addresses, just as if they were in the same region, while traffic never traverses the public internet.
  - The peering is non-transitive, requires explicit configuration on both sides, and incurs a modest inter-region data-transfer cost.

### Virtual Network Gateway

- **Virtual Network Gateway**: is a dedicated Azure resource that provides a secure tunnel endpoint for connecting an Azure Virtual Network to on-premise networks, other VNets, or remote clients via VPN or ExpressRoute.
  - It terminates the encrypted traffic, performs routing between the Azure VNet and the external network, and supports site-to-site, point-to-site, and VNet-to-VNet connectivity.
  - The gateway is provisioned as a specific SKU that determines throughput, supported features, and pricing.
  - Gateway Subnet is a second subnet that the network gateway is deployed in.

## Site-to-Site VPN

- **Site-to-Site VPN Gateway Connection**: is used to connect your on-premises network to an Azure virtual network over an IPsec/IKE VPN tunnel.
  - This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned to it.
  - You can create a site-to-site VPN connection by deploying the following steps:
    1. Deploy a virtual network
    2. Deploy a gateway subnet
       - You need to create a gateway subnet for your VNet in order to configure a virtual network gateway.  All gateway subnets must be named "GatewaySubnet" to work properly.  It is recommended for this subnet to be a /27 or larger.
    3. Deploy a VPN gateway
       -  **VPN Gateway**: is a specialized virtual network gateway used to establish encrypted communication between an Azure virtual network and an on-premises environment over the public internet.
    4. Deploy a local network gateway
    5. Deploy a VPN connection  

## Azure DNS

**Domain Name System (DNS)**: The way a human rememberable domain name is turned into an IP address.  
*For example*: microsoft.com -- resolves to  -> 40.112.72.205  
Four DNS options:
1. **You provide DNS (hosted elsewhere)**: the custom domain is resolved to an IP address before the traffic reaches Azure
2. **Azure Private DNS**: Not accessible for outside of Azure
   1. You do not need to register if with any registry
   2. Doesn't affect anything outside your own network
   3. **Enable Auto Registration**: enables automatic creation of DNS records in this private DNS zone, for the virtual machines connected to the virtual network.
3. **Azure Public DNS**: works like your registrar would
4. **Azure Domain Services**: register a domain to use for a Web App
   - This is the hosting service for DNS domains that provides name resolution by using Microsoft Azure infrastructure.  By hosting your domains in Azure, you can manage you DNS records by using the same credentials, tools, and billings as your other Azure services.

- **DNS Zone File**: is a text file that contains details of every DNS record in the zone.  It follows a standard format, making it suitable for transferring DNS records between DNS systems.
  - *Azure DNS supports importing and exporting zone fiels by using Azure CLI and Azure Portal only.  **NOT** supported via Azure PowerShell and Azure Cloud Shell.*


## Security Groups

- **Network Security Group (NSG)**: a core way to control network access in Azure. They act like a firewall using allow or deny rules, using things like IP address, port, and protocol.
  - Can be associated with either subnet or NIC
  - Rule based on priority, lower priority comes first
- **Application Security Groups (ASG)**: a logical grouping of resources that can be a destination.
  - Allows you to define network security rules based on application workloads rather than specific IP addresses.
  - Instead of creating security rules for individual VM IP addresses, you assign VMs to ASGs and then create Network Security Group rules that reference these groups.
  - *Key Benefit*: Makes security rules more manageable and scalable as your infrastructure grows.

## Load Balancers

- **Load Balancer**: device that (usually evenly) distributes traffic that comes in to multiple servers behind it.
  - Use it because while a single VM can suffice for non-critical workloads but there are downsides to using just a single server like:
    - Occasionally, you have to reboot the server for updates
    - Risk of a single rack, or data center, going offline
    - Risk of a lot of traffic all at once (*burst*)
- Two types of load balancers:
  - **Public Load Balancer**: accepts internet traffic and distributes it to backend VMs with public-facing IP
    - Used for web apps, APIs, and public-facing services
    - Remember the following concepts when attaching virtual machines to the backend pool of a load balancer:
      - The SKU of the IP address of a virtual machine must match the SKU of the load balancer.
      - You can attach virtual machines to the backend pool of a load balancer that does not contain an IP address.
      - You can attach virtual machines to the backend pool of a load balancer even if they are in a stopped state.
  - **Internal Load Balancer**: Accepts traffic within a VNet
    - Used for internal services, such as databases or internal apps
    - if you have a **Standard SKU** Internal load balancer you can load balance across VMs located in different subnets withing the same virtual network, which enhances the ability to manage traffic in larger, more distributed systems.
- **Azure Application Gateway**: is a web traffic load balancer that enables you to manage traffic to your web applications.  For example, you can route traffic based on the incoming URL.
  - So if /images are in the incoming URL, you can route traffic to a specific set of servers (known as a pool) configured for images.
  - If /videos is in the URL instead, you can route that traffic to another pool that's optimized for videos.
  - Also acts as a **Web Application Firewall** protecting web applications from common vulnerabilities and exploits, including:
    - SQL injections
    - Cross-site scripting attacks
    - Other common attacks, such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion
    - HTTP protocol violations
    - HTTP protocol anomalies, such as missing host user-agent and accept headers
    - Bots, crawlers, and scanners
    - Common application misconfigurations
- A standard load balancer supports:
  - **Zonal**: in one zone
  - **Zone-redundant**: across zones
- **Session Persistence**: also known as **session affinity** or **client IP affinity**.  Connections from the same client will go to the same backend instance within the backend pool.  Session persistence has two configuration types:
  - **Client IP (2-tuple)**: specifies that successive requests from the same client IP address will be handled by the same backend instance.
  - **Client IP and protocol (3-tuple)**: specifies that successive requests from the same client IP address and protocol combination will be handled bu the same backend instance.

## Network Watcher

- **Network Watcher**: is Azure's network monitoring and diagnostic service that helps troubleshoot connectivity issues and monitor network performance.  It is primarily used to diagnose why network connections aren't working and validate that your network security configurations are functioning as exposed.  It provides tools like: 
    - **Connection Monitor**: allows for tracking network connectivity over time
    - **IP Flow Verify**: to check if traffic is allowed or denied by security rules
    - **Next Hop**: to trace network routing paths
    - **NSG Flow Logs**: allows you to view information about traffic flowing through an NSG
    - **Next Hop**: allows you to trace the next hop for a given network destination.  This is useful for diagnosing issues with User Defined Routes (static routes)