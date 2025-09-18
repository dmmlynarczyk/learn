## Lab 05: Intersite Connectivity - Connecting Azure Networks

**What This Lab Taught Me**:
Learning to create virtual network peering to enable communications between resources in different virtual networks - basically making separate Azure networks talk to each other securely.

**Core Network Connectivity Concepts**:
- **VNet Peering**: Created automatic bidirectional peering connections between virtual networks with "Connected" status
- **Cross-Network Communication**: VMs in different networks can now communicate as if they're on the same network
- **Network Isolation vs Connectivity**: Understanding when to keep networks separate vs when to connect them

**Real-World Network Architecture**:
Virtual network peering allows multiple networks to communicate securely, while network security groups and custom routes help ensure secure and controlled traffic flow - this is how companies connect different departments or applications.

**What Clicked for Me**:
- **Peering vs Internet**: Traffic stays within Azure's backbone instead of going over the public internet
- **Bidirectional Setup**: Peering automatically creates connections on both virtual networks
- **Regional Flexibility**: Can connect networks in same region or across different Azure regions

**Practical Network Testing**:
- **Connectivity Verification**: Actually tested that VMs could communicate across the peered networks
- **Network Troubleshooting**: Used Network Watcher and PowerShell tools for diagnosing connectivity
- **Security Validation**: Confirmed that security groups still controlled what traffic was allowed

**Navigation Learning**:
- Found peering settings under each VNet's configuration
- Network topology visualization helped understand the connections
- Monitoring tools showed actual traffic flow between networks

**Business Context**:
This solves the problem of connecting different application tiers, departments, or environments (dev/test/prod) while maintaining network security and performance.

**Key Insight**: 
Network peering is about controlled connectivity - you can connect networks without making them completely open to each other, maintaining security boundaries while enabling necessary communication.
