## Lab 08: Virtual Machines - High Availability & Scaling

**What This Lab Taught Me**:
Learning to deploy VMs across availability zones for high availability, resize VMs, add disks, and scale with VMSS to optimize performance and reduce administrative overhead

**Core VM Management Concepts**:
- **Availability Zones**: Deploying VMs into different availability zones for redundancy - if one zone fails, others keep running
- **VM Scaling**: Adjusting VM size/SKU to get more (or less) compute and memory when needed
- **Scale Sets vs Individual VMs**: Understanding when you need multiple identical VMs vs just one bigger VM

**Real-World Infrastructure Thinking**:
- **High Availability**: Why you'd spread VMs across zones instead of putting them all in one place
  - You achieve a 99.99% uptime SLA because you have at least two VMs distributed across at least two zones.
  - In the scenario where you might only need one VM, it is a best practice to still deploy the VM to another zone.
- **Cost vs Performance**: Scaling up when you need power, scaling down to save money
- **Automation**: Scale Sets can automatically add/remove VMs based on demand

**What Made Sense**:
- **Zone Resilience**: If a data center has issues, my application keeps running in other zones
- **Flexible Scaling**: Different orchestration modes (Uniform vs Flexible) affect scaling options
- **Resource Management**: Adding disks and resizing without rebuilding the entire VM

**Practical Challenges**:
- **Zone Selection**: Had to think about which zones to use and why
- **VM Sizing**: Understanding what "Standard_B2s" vs other sizes actually means for performance
  - I made a basic Standard_B1s with 1 vCPU, 1 GiB memory and was unable to launch a web browser and server manager at the same time. Even IIS refused to start properly!
- **Scale Set Configuration**: Lots of options for how aggressive the auto-scaling should be

**Navigation Learning**:
- Virtual Machine Scale Sets have their own section (not just under regular VMs)
- Monitoring showed me actual resource usage to help decide when to scale
- Network configuration was more complex with multiple VMs

**Business Context**:
This isn't just about creating VMs - it's about building reliable, scalable infrastructure. Real companies need systems that stay online during outages and can handle traffic spikes automatically.

**Key Insight**: 
Building resilient infrastructure means planning for failure from the start. It's easier to design for high availability than to add it later.
