# Manage Azure Identities and Governance

**20%-25% of AZ-104 exam.**  

- [Manage Azure Identities and Governance](#manage-azure-identities-and-governance)
  - [Entra ID Basics](#entra-id-basics)
  - [License Tiers](#license-tiers)
  - [Domains](#domains)
  - [Groups](#groups)
  - [Licenses](#licenses)
  - [Administrative Units](#administrative-units)
  - [Devices](#devices)
  - [Self-Service Password Reset](#self-service-password-reset)
  - [Role Based Access Control (RBAC)](#role-based-access-control-rbac)
    - [Benefits of RBAC](#benefits-of-rbac)
    - [Role Types](#role-types)
    - [Interpret Access Assignments](#interpret-access-assignments)
  - [Accounts, Subscriptions, and Governance](#accounts-subscriptions-and-governance)
    - [Cost Management - Analysis, Alerts, Budget, and Advisor](#cost-management---analysis-alerts-budget-and-advisor)
    - [Resource Locks](#resource-locks)
    - [Azure Policies](#azure-policies)
      - [Non-Compliant Policies](#non-compliant-policies)
    - [Tags](#tags)
    - [Azure Advisor](#azure-advisor)


## Entra ID Basics

> [!NOTE]
> Azure AD is now called Entra ID.  
> Any time you see Azure AD in studying, it should be Entra ID

**Microsoft Entra ID:** is Microsoft's cloud-based identity and access management service that handles user authentication and authorization for Azure resources.  
It is derivative of **Microsoft Active Directory**, which is their on-premises service for managing users, computers, and resources.

## License Tiers

- **Microsoft Entra ID Free:** No SLA, AI, and other advanced features, but great for most basic users just starting out
  - Basic user/group management, SSO to popular apps
- **Microsoft Entra ID P1:** Includes some advanced features
  - Conditional access, dynamic groups, self-service password reset
- **Microsoft Entra ID P2:** Includes everything in P1 and more advanced features
  - Identity protection, privileged identity management, and *Microsoft Entra ID Protection*
- **Microsoft Entra ID Governance:** Add-on license, you must have a P1 or P2 already

## Domains

If you choose not to add a custom domain you will be stuck with a <domain>.onmicrosoft.com style domain, which is the generic Microsoft domain space.  If you do want to add a custom domain, you will need to add either a **TXT** or **MX** record to your domain registrar records page to show you have ownership of that domain.   

## Groups

Groups are simply a way to organize based on a fixed assignment or on a dynamic property.  
When creating groups you have the option to *allow Azure AD roles to be assigned to the group.*  This allows you to use the group as a way to assign permissions.  The group is just an organizational structure.  

**Dynamic Groups:** are groups that are assigned members automatically based on certain criteria being met. *(If user position is X, location is Y, department is Z, etc.)*

**Assigned Groups:** are groups that have members set by the administrator manually.

## Licenses

> [!NOTE]
> Adding, removing, and reprocessing licensing assignments is only available within the M365 Admin Center.  

Certain good features are locked behind a license such as "Self-Service Password Change for cloud users."  Instead of users being able to change their passwords on their own, like the license would allow, users would have to call in to the help desk instead.  
Items such as "Multifactor authentication for administrator roles" is part of the free tier, so it allows your admin accounts to at least be secure.  This is only for the authenticator app though, things like SMS and Phone MFA are through a license.  
Licenses may not be able to be assigned without a 'Usage Location' listed in the user's information.  

## Administrative Units

**Administrative Unit:** is a resource inside of Entra that can act as a container for other resources.  It can contain only users, groups, or devices.  
It is a way of segregating permissions into a logical separation.  So certain users can only affect certain parts of the organization instead of the entire organization.  

In my lab example, Teacher1 is a *Password Administrator* for Classroom1.  He can reset passwords for any person in Classroom1, but not in any other classroom.  Student1 is a user inside of Classroom1, so he is the only person that can have their password reset by Teacher1.  An interesting thing is that we can also add groups to the assignment, so if we added a *Student Group* to Classroom1, then teacher1 could reset passwords for anyone inside of that group.  A container inside a container.  

## Devices

**Devices:** represent the physical devices that users use to access organizational tools, information, and resources.  My cellphone and home computer are devices that access my company's resources.  
In devices section you can set things like, don't allow rooted/jailbroken devices or insecure devices to access resources.  

## Self-Service Password Reset

Password reset is available to administrative users already, but not for other users without special licensing.  
By default self service password reset is set to 'None', but there are three options to choose from:
- **None:** no one can reset their password by themselves, and users must call in to help desk.  
- **Selected:** limited to a specific group of users.  
- **All:** all users are able to reset their passwords themselves.  
This essentially just allows the user to hit the "Forgot Password" option on the Azure login screens.  

**Password Pushback:** should be enabled for a company that is AD Sync'd.  This allows a user to change their password for Azure/M365 and it will push into the on-prem Active Directory.  

## Role Based Access Control (RBAC) 

**Role Based Access Control (RBAC):** is a security feature in Azure that allows you to grant specific permissions to different Azure entities based on their ROLES in your organization.  
At a basic level, "in order for a user to interact with a resource in Azure, you need permissions."  With 10,000s of users, and 1,000s of resources, it quickly becomes impossible to manage properly.  There could be literally millions of permissions that need to be worked on when all is said and done.  

RBAC allows you to define a number of "roles" across the organization that you can then assign those roles to individuals.  Those roles have a static number of permissions, meaning you do not have to worry about giving access to too much.  As long as the role is setup properly, the user will be given least access permissions.  
Users *CAN* be assigned to multiple roles.  

RBAC is primarily used to manage who can do what on which resources.  It **does not** provide granular control over the properties or configuration details of resources being created, such as enforcing restrictions for VM SKU size, etc.  

>[!NOTE]
> RBAC is focused on authorization and access management, not financial tracking.

### Benefits of RBAC

- A level of abstraction the helps to simplify management
- This means fewer errors, and nobody has extra permissions that may be overlooked.
- Easier for new users to be added to the system and assigned the correct permissions.

### Role Types

To adhere to the principle of least privilege, we must select a role that provides exactly the necessary permissions without granting excessive access.  Roles can be used to fine tune access to resources, there are three built-in roles that include:
- **Owner:** Grants full access to manage all resources, including the ability to assign roles in Azure RBAC.  
- **Contributor:** Grants full access to manage all resources, *but does not allow you to*: 
  - assign roles in Azure RBAC
  - manage assignments in Azure Blueprints
  - share image galleries
  - assign or manage POSIX ACLs
- **Reader:** View all resources, but does not allow you to make any changes.  

**You can also make custom roles!**  
To do this you need to have an Azure Premium P1/P2 to gain access to custom roles.  But it will allow you to get super-granular into permissions to pick and choose specifics.  
This is done at the Subscription level under IAM > "+ Custom Role"  

### Interpret Access Assignments

You can view who has access to different resources, by going into that resource group, clicking "Access Control (IAM), clicking "role assignments", and you will be presented with a list of users with different roles.  
The other way is be selecting the user in Entra ID and selecting either "Azure role assignments" or "Assigned roles"  

## Accounts, Subscriptions, and Governance

- **Account:** a user ID, so it is a person or an app (managed identity).
  - It is considered a bad practice to take a peron's real credentials and program them into an application.
- **Tenant** is a representation of an organization
  - Typically represented bya  public domain, but will be assigned a .onmicrosoft.com domain if not specified
  - A dedicated instance of **Entra ID**
  - **Every Azure Account is part of at least one tenant**  
- **Subscription** is an agreement with Microsoft to use Azure services, and how you will pay for that usage
  - All Azure resource usage will be billed to the payment method of the subscription
  - Not every tenant has a subscription, but a tenant without one, will not be able to create Azure resources
  - Tenants can have more than one subscription
  - More than one account can be the owner in a tenant
- **Resource** is any entity managed by Azure
  - Accounts can be given read, update, owner rights to resources
- **Resource Group** is a container that holds related resources and allows for keeping unrelated resources separate
  - It is a way of organizing resources in a subscription
  - Think of it like a folder structure
  - **All resources must belong to only one resource group**
  - When you delete a resource group, it will also delete all resources inside
  - To verify the date and time the resources were deployed, you can select the resource group and click the deployment settings. You will see a summary of the deployment including: 
    - deployment name
    - status
    - last modified
    - duration
    - related events
  - If you select the specific template, you can check the inputs, outputs, and the template used during deployment.

### Cost Management - Analysis, Alerts, Budget, and Advisor

If you ever want to see how your account is being billed it is easiest to go under "Subscription" to **"Cost Management"** where you can view your "cost analysis", "Cost alerts", "Budgets", and "Advisor recommendations."  
- **Cost Analysis:** this is going to tell you in detail how we are accumulating costs, which resources are using them, what the cost forecast for the end of the billing period is, etc.
- **Cost Alerts:** allows you to set up alerts based on certain thresholds based on what you are expected to spend.
  - Also allows you to set up cost anomaly alerts.
- **Budgets:** allows you to set an alert (SMS, email) when your monthly expenditure has hit certain thresholds.  Such as percentage of a budget being reached.
- **Advisor Recommendations:** runs across your account and makes recommendations across categories, including costs!

### Resource Locks

**Azure Resource Locks**: are primarily used to prevent accidental deletion or modification of existing critical resources.  There are two types of locks:
- **ReadOnly:** prevents a resource from being modified AND deleted.  You cannot make ANY changes to ANY resource the lock is applied to.
- **Delete:** prevents a resource from being deleted, but can still be modified.

The lock will need to be removed before you can modify/delete your resource that the lock is applied to.  Can be applied to subscription, resource group, and individual resources!

### Azure Policies

**Policy Definition:** is a blueprint or template that describes what should be evaluated and what action to take.  It defines the rules and logic 

**Policy:** is an instance of a policy definition that has been assigned to a specific scope.  This is the policy definition put into action with specific parameters and enforcement settings.  

**Initiative:** is a collection of policies, so you can batch assign a group of related policies if you need.  

> [!NOTE]
> You would use policies to enforce creation rules like:
> - only logins from location XYZ are allowed
> - what version of SQL server you are allowed to deploy
> - which VM SKU sizes are allowed.

To create, update, delete, and query Azure Policy Definitions you can use the following:
- Azure Portal
- Azure PowerShell
- Azure CLI
- ARM templates
- Azure Policy REST API


**Policy effects** help to enforce compliance by blocking deployments that do not meet policy requirements, and the **Audit Effect** can log non-compliance for review.  If you apply a policy to a subscription it will apply to all deployments under that subscription.  It is important to determine the scope you need the policy assigned to.  

*Example*: if you had a policy to deny the creation of virtual network interfaces, and you tried to create a VM, the VM deployment would fail because the policy will deny the creation of the required resources.  It will be denied at the validation phase before any resources can be provisioned for creation.

> [!IMPORTANT]
> While Azure Policies will prevent certain actions and block updates if they would violate a policy rule, *it will not* automatically deallocate or stop an already running instance, such as a VM.  You will have to do that manually.

#### Non-Compliant Policies

To bring non-compliant resources into compliance by using Azure Policy's remediation capabilities you would need to do the following:
1. Access the "Compliance" blade under Azure Policy
2. Create and Initiate a Remediation Task
3. Specify remediation task details
4. Review the remediation task details and click "Remediate" to start the process

### Tags

Tags allow you to define a name/value pair that can be attached to resources. They are specifically designed for categorization, management, and cost allocation.
Important to keep it consistent in your organization to ensure things are easy to find/determine. 
You could set policies to require tags for all different types of things in Azure.  Subscriptions, resource groups, resources, etc. 

If you consistently apply proper tags (such as a Department tag) to all resources, you can easily break down and attribute costs to individual departments, enabling effective chargeback and budget management.

### Azure Advisor

**Azure Advisor**: is your go-to personalized cloud consultant, dedicated to helping you optimize your Azure deployments for maximum efficiency.  By thoroughly analyzing your resource configurations and monitoring usage data, Azure Advisor delivers tailored recommendations that enhance various aspects of your cloud environment.  

Azure Advisor is specifically designed to provide personalized, actionable recommendations for your Azure resources. It helps users follow best practices and optimize their Azure deployments.  

Its recommendations cover five key pillars:
1. Cost
2. Security
3. Reliability
4. Operational Excellence
5. Performance  

These suggestions focus on improving *cost-effectiveness, boosting performance, ensuring reliability,* and *fortifying security,* allowing you to maximize the value of your Azure resources while minimizing potential risks.  
