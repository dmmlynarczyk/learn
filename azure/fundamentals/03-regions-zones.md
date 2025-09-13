# Azure Regions and Availability Zones

## What There Are

- **Region:** Geographic area with multiple datacenters (*and multiple Availability Zones*)
  - Microsoft Azure offers geographically dispersed data centers, allowing data to be replicated in multiple locations. This ensures that if a natural disaster impacts one data center, data is still accessible from another location
- **Availability Zone:** Separate datacenter within a region
  - The goal for Azure is for all regions to have multiple AZs
- **Region Pair:** Two Regions paired together for disaster recovery
  - Usually are 100's of miles apart, so a major event in one part of a country does not bring everything down  

## Availability Zone Support

- **Zone-redundant deployment:** are replicated across multiple Availability Zones automatically.  This means a failure in one zone will not affect other AZs.
- **Zonal deployment:** deployed to a single AZ.  This provides no resiliency but helps lower latency and improve other performance metrics.