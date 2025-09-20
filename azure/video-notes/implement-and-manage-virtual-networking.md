# Implement and Manage Virtual Networking

15%-20% of AZ-104 exam.  

## Virtual Networks

**Virtual Networks**: are your private network space in the cloud that logically isolates your Azure resources from other customers.  They work like a traditional network in your office - you can control IP addresses, create and modify subnets, set up security rules, and connect to other network or the internet, giving you secure communication between your Azure resources.  

### Security Settings

- **Virtual Network Encryption**: to encrypt traffic traveling within the virtual network.
  - Traffic to public IP addresses is not encrypted.
  - Your VMs must have accelerated networking enabled.
- **Azure Bastion**: *PAID SERVICE* that provides secure RDP/SSH connectivity to your virtual machines over TLS.
  - When you connect via Bastion your VMs do not need a public IP address.
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

## VNET Peering

- By default any server running on a virtual network will not be able to communicate with a server on a different virtual network.  They will be able to talk to servers on the same virtual network though.
- **Peering**: is the idea of setting up a relationship on two different virtual networks that they recognize each other.  Allowing virtual machines running on one vnet will be able to communicate with virtual machines on another vnet.
> [!IMPORTANT]
> The IPs defined in one virtual network have to be non-overlapping.

- Vnets can have peerings with multiple other vnets.  Think hub and spoke topology.
- **Traffic to remote virtual network**: this will need to be allowed if you wish to allow communication between the two virtual networks.
  - This option allows the remote virtual network address space to be included as part of the Virtual_Network tag.
- **Traffic forwarded from remote virtual network**: this setting allows forwarded traffic from remote virtual network (traffic not originating from inside remote virtual network) into NewTest1. 
  - This allows a hub and spoke topology to actually forward non-peered network together.
- If you know the Resource ID of two different resources in different subscriptions you can peer them together also!

### Global Peering

> [!NOTE]
> Both ingress and egress traffic is charged at both ends of the peered networks.

- **Global Peering**: connects two Azure virtual networks that reside in **different Azure regions** (or subscriptions) so they can communicate privately over Microsoft's backbone network.  
  - Once peered, resources in either vnet can reach each other using their private IP addresses, just as if they were in the same region, while traffic never traverses the public internet.
  - The peering is non-transitive, requires explicit configuration on both sides, and incurs a modest inter-region data-transfer cost.

### Virtual Network Gateway

- **Virtual Network Gateway**: is a dedicated Azure resource that provides a secure tunnel endpoint for connecting an Azure Virtual Network to on-premise networks, other vnets, or remote clients via VPN or ExpressRoute.
  - It terminates the encrypted traffic, performs routing between the Azure vnet and the external network, and supports site-to-site, point-to-site, and vnet-to-vnet connectivity.
  - The gateway is provisioned as a specific SKU that determines throughput, supported features, and pricing.
  - Gateway Subnet is a second subnet that the network gateway is deployed in.

## Azure DNS

**Domain Name System (DNS)**: The way a human rememberable domain name is turned into an IP address.  
*For example*: microsoft.com -- resolves to  -> 40.112.72.205  
Three DNS options:
1. **You provide DNS (hosted elsewhere)**: the custom domain is resolved to an IP address before the traffic reaches Azure
2. **Azure Private DNS**: Not accessible for outside of Azure
   1. You do not need to register if with any registry
   2. Doesn't affect anything outside your own network
   3. **Enable Auto Registration**: enables automatic creation of DNS records in this private DNS zone, for the virtual machines connected to the virtual network.
3. **Azure Public DNS**: works like your registrar would
4. **Azure Domain Services**: register a domain to use for a Web App

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
  - **Internal Load Balancer**: Accepts traffic within a VNet
    - Used for internal services, such as databases or internal apps
- A standard load balancer supports:
  - **Zonal**: in one zone
  - **Zone-redundant**: across zones
- 