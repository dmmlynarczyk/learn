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