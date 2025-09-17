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