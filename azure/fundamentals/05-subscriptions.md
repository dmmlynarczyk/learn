# Subscriptions and Management Groups

## Subscriptions

**Subscription:** is an agreement between a customer and Microsoft on how to pay for and access Azure services.  
Paid based on what services are consumed.  

## Management Groups

**Management Groups:** provide a way to organize your subscriptions by adding hierarchies to Azure.  They also allow you to assign permissions and limits to different groups of people on each Azure service they use.  
You should use management groups if you plan to deploy multiple subscriptions for multiple departments from your organization.  

**Role-Based Access Control (RBAC):** is used to provide different access levels to Azure services
  - **Provides a way to control who can access various Azure resources**
- Typical Azure RBAC roles are:
  - **Owner:** Grants full access to manage all resources, including the ability to assign roles in Azure RBAC
  - **Contributor:** Grants full access to manage all resources but *does not* allow you to assign roles in Azure RBAC, manage assignments in Azure Blueprints, or share image galleries.
  - **Reader:** Only allows you to view resources, does not allow you to make any changes
  - **User Access Administrator:** Lets you manage user access to Azure resources.

