# Resource Groups

## What Are Resource Groups?

- Containers that hold related Azure resources
- Avery object in Azure belongs to exactly one resource
- Think of it like a file system for organizing your Azure resources
- This is a logical grouping, and is not based on physical location

## Key Concepts

### Resource Group Properties

- **Location:** Metadata storage location (not where resources live)
- **Lifecycle:** Deleting a resource group will delete all of the resources inside of it
- **Permissions:** RBAC applied to a resource group will apply to all resources in that resource group
- **Tags:** Can be applied to resource groups and be inherited down to resources

### Resource Group Scope

- Resources can be in different regions than their resource group
- Resource in the same resource group can be in different regions
- Resource group location only affects where metadata is stored
- **Resource groups cannot be nested inside of other resource groups**

### Resource Movement

- You can move most resources between resource groups
  - However there are a few that cannot be moved
- Moving resources will not change the configuration of the resources, but it may cause a brief amount of downtime during the move

## Naming Conventions

- Use descriptive and consistent names
- If they do exist follow existing company standards
- if making from scratch include:
    - Environment: `rg-webapp-prod` or `rg-webapp-dev` to show whether it is development or production environment
    - Purpose: `rg-networking-hub` or `rg-storage-backup` to easily identify what it is used for

## Permissions and RBAC

> [!IMPORTANT]
> **Permissions assigned to a resource group will apply to all resources inside of the resource group**


## Important Commands

### PowerShell

``` powershell
# Create resource group
New-AzResourceGroup -Name "rg-webapp-prod" -Location "East US"

# List resource groups
Get-AzResourceGroup

# Get resources in a group
Get-AzResource -ResourceGroupName "rg-webapp-prod"

# Delete resource group (and all resources)
Remove-AzResourceGroup -Name "rg-webapp-prod" -Force

# Move resource to different group
Move-AzResource -ResourceId "/subscriptions/.../resourceGroups/source-rg/providers/Microsoft.Compute/virtualMachines/vm1" -DestinationResourceGroupName "target-rg"
```

### CLI

```bash
# Create resource group
az group create --name rg-webapp-prod --location eastus

# List resource groups
az group list --output table

# Show resources in group
az resource list --resource-group rg-webapp-prod --output table

# Delete resource group
az group delete --name rg-webapp-prod --yes --no-wait

# Move resource
az resource move --destination-group target-rg --ids /subscriptions/.../resourceGroups/source-rg/providers/Microsoft.Compute/virtualMachines/vm1
```


