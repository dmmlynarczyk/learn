## Lab 04: Virtual Networking - Building Secure Network Foundation

**What This Lab Taught Me**:
Learning to design and implement core Azure networking infrastructure including virtual networks, IP addressing schemes, subnets, and network security groups - basically building the network foundation that everything else sits on.

**Core Networking Concepts I Grasped**:
- **VNet Structure**: Understanding how to configure virtual networks and subnets with proper IP addressing
- **Network Security Groups**: Created NSGs with inbound rules allowing specific traffic and outbound rules denying internet access
- **Application Security Groups**: Used ASGs to group similar resources and apply security rules based on application function rather than IP addresses

**Security Architecture I Learned**:
- **Defense in Depth**: NSGs control traffic flow to and from subnets and VMs since there aren't security boundaries by default between subnets
- **Rule-Based Access**: Allow only necessary traffic, deny everything else by default
- **Application-Based Grouping**: Group VMs by function (web servers, database servers) rather than network location

**What Made Network Security Click**:
- **Default Behavior**: Virtual machines in subnets can communicate by default - NSGs add the security boundaries
- **Layered Protection**: NSGs can be applied at both subnet and individual VM levels
- **Traffic Direction**: Understanding inbound vs outbound rules and how they work together

**Practical Network Design**:
- **IP Address Planning**: Choosing subnet ranges that don't overlap and allow for growth
- **Security Rule Priority**: Learning how rule order and priority numbers affect which rules apply
- **Application Grouping**: ASGs make it easier to manage security for groups of similar servers

**Real-World Context**:
This isn't just creating networks - it's building secure, scalable network architecture that supports business applications while controlling access and preventing unauthorized communication.

**Key Insight**: 
Network security in Azure is about intentional design - you build the network structure first, then layer on security controls to match your business requirements and security policies.
