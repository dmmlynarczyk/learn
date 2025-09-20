## Lab 06: Network Traffic Management - Load Balancing & Application Routing

**What This Lab Taught Me**:
Learning to implement Azure Application Gateway for layer 7 load balancing with Web Application Firewall (WAF), SSL termination, and end-to-end encryption, plus Azure Load Balancer for distributing traffic across multiple VMs.

**Traffic Management Concepts I Grasped**:
- **Layer 4 vs Layer 7**: Load Balancer works at layer 4 (network level) while Application Gateway works at layer 7 (application level)
- **Path-Based Routing**: Application Gateway can route traffic based on URL paths like /image/* to specific backend pools
- **High Availability**: Both services distribute traffic to prevent single points of failure

**Real-World Application Architecture**:
- **Web Application Protection**: Application Gateway provides Web Application Firewall (WAF) protection against common web attacks
- **SSL Management**: Centralized SSL termination instead of managing certificates on each VM
- **Performance**: Traffic distribution and path-based routing improve user experience

**What Clicked for Me**:
- **Different Use Cases**: Load Balancer for general traffic distribution, Application Gateway for web applications with advanced features
- **Backend Pool Concept**: Both services route to groups of servers, not individual ones
- **Health Probes**: Services automatically detect unhealthy servers and stop sending traffic

**Practical Configuration Learning**:
- **Subnet Requirements**: Application Gateway needs its own subnet sized /27 or larger
- **Public IP Management**: Frontend IP configuration with public IP addresses
- **Rule Configuration**: Setting up routing rules and backend pool associations

**Business Context**:
This isn't just about distributing traffic - it's about building resilient, secure web applications that can handle growth and protect against attacks while maintaining performance.

**Key Insight**: 
Traffic management is about more than just spreading load - it's about intelligent routing, security, and ensuring users always reach healthy, responsive servers.
