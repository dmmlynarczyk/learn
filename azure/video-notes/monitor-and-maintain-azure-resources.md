# Monitor and Maintain Azure Resources

10%-15% of AZ-104 exam.  

- [Monitor and Maintain Azure Resources](#monitor-and-maintain-azure-resources)
  - [Monitor Resources In Azure](#monitor-resources-in-azure)
    - [Insights](#insights)
    - [Data Collection Endpoints](#data-collection-endpoints)
    - [Detection, Triage, and Diagnostics](#detection-triage-and-diagnostics)
    - [Azure Advisor](#azure-advisor)
  - [Implement Backup and Recovery](#implement-backup-and-recovery)
    - [Standard vs Enhanced Backup](#standard-vs-enhanced-backup)
    - [Azure Site Recovery](#azure-site-recovery)
    - [Recovery Services Vault](#recovery-services-vault)


## Monitor Resources In Azure

In the sidebar and in the resources it is simply called **Monitor**.  
**Azure Monitor**: is a centralized dashboard that contains all of the diagnostics, logging, and metrics for associated services.  

### Insights

Monitor contains insight metrics for 18 different services, but some of the more important ones for now are:
- **Application Insights**: monitor your app's availability, performance, errors, and usage
- **Container Insights**: gain visibility into the performance and health of your controllers, nodes, and containers
- **VM Insights**: monitor the health, performance, and dependencies of your VMs and VM scale sets
- **Network Insights**: view the health and metrics for all deployed network resources
- **Storage Account Insights**: Performance, capacity, and availability of storage accounts
- **Connection Monitor**: provides unified, end-to-end connection monitoring in Azure Network Watcher.  can be used to compare latencies of on-premises site to the latencies of an Azure application.
- **IP Flow Verify**: allows your to detect traffic filtering issues at a VM level.
- **Packet Capture**: allow syou to capture traffuc on a VM in a virtual network.
- **Traffic Analysis**: primarily used to examine NSG flow logs in order to provide insights into traffic flow.

### Data Collection Endpoints

- **Data Collection Endpoint (DCE)**: is a component designed to manage and secure the flow of telemetry data from your resources from your resources to Azure Monitor.
  - It provides a dedicated endpoint for collecting logs, metrics, and traces from various Azure services and applications.

### Detection, Triage, and Diagnostics

Monitor allows for the visualization, analysis, and responding to monitoring data and events, some of these include:
- **Metrics**: create charts to monitor and investigate the usage and performance of your Azure resources
- **Alerts**: Get notified and respond using alerts and actions
- **Logs**: Analyze and diagnose issues with log queries
- **Health Model**: manage the health of your full-stack applications and workloads

### Azure Advisor

- **Azure Advisor**: is a personalized cloud consultant that helps you follow best practices to optimize your Azure deployments.
  - It analyzed your resource configuration and usage telemetry and then recommends solutions that can help you improve the cost-effectiveness, performance, reliability, and security of your Azure resources.
  - You can optimize and improve the efficiency of your infrastructure by identifying idle and underutilized resources.
  - Azure Cost Management works with Azure Advisor to provide cost optimization recommendations.

## Implement Backup and Recovery

- **Azure Backup**: a cloud-based backup service that protects data and applications running in Azure VMs, on-premises servers, and other Azure services like SQL databases and file shares.
  - It provides centralized backup management through Recovery Services vaults, offers point-in-time recovery with configurable retention policies, and includes features like incremental backups to minimize storage costs.
  - *It is essential for implementing data protection strategies, configuring backup policies for VMs and workloads, and understanding disaster recovery planning.*
- **Soft Delete**: your data is protected from permanent deletion for a set period. 
  - Enabled by default on new Recovery Services Vault (RSV)
  - 14 days to delete backup data
  - Cen be un-deleted
  - 15th day - auto delete

### Standard vs Enhanced Backup

| **Standard**                    | **Enhanced**                                           |
|:-------------------------------:|:------------------------------------------------------:|
|   Once a day backup             |   Multiple backups per day                             |
|   Up to 5 days operational tier |   Up to 30 days operational tier                       |
|----------------------------     |   Support for VMs with Ultra Disks and Premium SSD v2  |
|----------------------------     |   Support for Trusted Launch Azure VM                  |

### Azure Site Recovery

**Azure Site Recovery (ASR)**: is a disaster recovery service that replicates workloads from a primary site to a secondary location, enabling continuity during outages or disasters.  
- It can replicate Azure VMs between regions, on-premises VMs to Azure, or between on-premises sites, with automated failover and failback capabilities.
- It is used to implement comprehensive disaster recovery plans, ensure RPO/RTO requirements are met, and provide business continuity for critical applications and infrastructure.

### Recovery Services Vault

- **Recovery Services Vault**: an entity that stores the backups and recovery points created over time *for a particular Region only*.  
  - The data is typically copies of data, or configuration information for viertul machines (VMs), workloads, servers, or workstations.
  - You can use Recovery Services vaults to hold backup data for various Azure services, and they make it easy to organize your backup data while minimizing management overhead.
> [!NOTE]
> You can only backup data sources or VMs that are in the same region as the Recovery Services vault.  You can back up VMs that have different resource groups or OS's as long as they are in the same region as the vault.

**When performing a failover you should**:
1. **Verify the VM settings**: check if the VM is healthy and protected.
2. **Run a failover**: in the failover tab, you are required to choose a recovery point.
3. **Reprotect the VM**: after failover, you re-protect the VM in the secondary region so that it replicates back to the primary region.
