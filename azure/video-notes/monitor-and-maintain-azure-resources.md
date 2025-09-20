# Monitor and Maintain Azure Resources

10%-15% of AZ-104 exam.  

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

### Detection, Triage, and Diagnostics

Monitor allows for the visualization, analysis, and responding to monitoring data and events, some of these include:
- **Metrics**: create charts to monitor and investigate the usage and performance of your Azure resources
- **Alerts**: Get notified and respond using alerts and actions
- **Logs**: Analyze and diagnose issues with log queries
- **Health Model**: manage the health of your full-stack applications and workloads

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

| **Standard**                | **Enhanced**                   |
|:---------------------------:|:------------------------------:|
|   Once a day backup         |   Multiple backups per day     |
|   1-5 days operational tier |   1-30 days operational tier   |
|   Vault tier                |   Vault tier                   |
|---------------------------- |   ZRS resilient snapshot tier  |
|---------------------------- |   Support for Trusted Azure VM |

### Azure Site Recovery

**Azure Site Recovery (ASR)**: is a disaster recovery service that replicates workloads from a primary site to a secondary location, enabling continuity during outages or disasters.  
- It can replicate Azure VMs between regions, on-premises VMs to Azure, or between on-premises sites, with automated failover and failback capabilities.
- It is used to implement comprehensive disaster recovery plans, ensure RPO/RTO requirements are met, and provide business continuity for critical applications and infrastructure.
