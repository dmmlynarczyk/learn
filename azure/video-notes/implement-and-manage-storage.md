# Implement and Manage Storage

15%-20% of AZ-104 exam.  

## Create Storage Accounts

When creating a storage account it is important to remember that the region that you choose will directly affect the amount you pay.  But you want the data to live close to you for accessing.  Region can also be chosen based on the jurisdiction of the data you are storing.  For example, health data for U.S. patients, need to be stored in the U.S.  

### Redundant Storage

> [!NOTE]
> Not all redundancy options are available in all regions.

The data in your Azure storage account is always replicated (*copied three times*) to ensure durability and high availability, but there are different methods on how and where that data is replicated to. 
- **Locally-redundant storage (LRS)**: Has basic protections against server rack and drive failures.
  - Lowest cost option.
  - Stored in one region/one data center
  - Recommended for non-critical scenarios.
- **Geo-redundant storage (GRS)**: Intermediate option with failover capabilities in a secondary region.
  - Recommended for backup scenarios.
  - Takes your data out to another region.
    - So three copies in a datacenter in your region and three copies of your data in another region.
- **Zone-redundant storage (ZRS)**: Intermediate option with protection against datacenter-level failures.
  - Recommended for high availability scenarios.
  - Spreads across three datacenters across one region.
- **Geo-zone-redundant storage (GZRS)**: Optimal data protection solution that includes the offerings of both GRS and ZRS.
  - Recommended for critical data scenarios.
  - Three copies of your files in three different datacenters in two different regions.
  - **This is the safest option if you NEED your data safe.**

### Advanced Options

Just like in AWS, Azure has an option to allow/disallow anonymous access on individual storage containers.  It is best to leave it off (*Default*) as this will greatly reduce an accidental leak of anything in your storage accounts.  

The default version are set, because they are typically the best options, and shouldn't be altered unless you have specific reasons for altering.  

### Blob Storage Access tiers

**Access Tier**: is the default tier that is inferred by any blob *without an explicitly set tier*
- **Hot**: Optimized for frequently accessed data and everyday usage scenarios (*Default*)
- **Cool**: Optimized for infrequently accessed data and backup scenarios
- **Cold**: Optimized for rarely accessed data and backup scenarios
- **Archived**: Can only be set at the blob level and not on the account.  VERY SLOW to get your data otherwise VERY EXPENSIVE for priority retrieval.


### Networking

There are three ways you can connect to your storage account:
- By default storage accounts have public internet access, so anyone, anywhere in the world can access the storage account data if they have the public URL and they have the Access Key!  
- If that gives you uneasy-ness, you can choose to only allow from selected virtual networks and IP addresses.  
- Otherwise you can disable all public access and only allow for private access.  
  - By choosing this option you can create a private endpoint to allow a private connection to your resource.

### Data Protection

**Data Protection**: Keeps your data protected from accidental or erroneous deletion or modification of files.  
**Point-in-time restore**: allows you to restore a container to an earlier state in time.  
**Soft Delete**: when you go to delete a file, it will mark is as 'marked for deletion' and not actually delete it.  You will then have a number of days, specified by you, to retrieve the file before it is actually deleted.  
**Tracking**: Allows you to keep track of changes made to your blob data.  
**File immutability**: means that you have a file that can never be deleted or edited, and you can be certain that it has not been changed.  

## Encryption

There are two encryption types in Azure:
- **Microsoft-managed keys**: where Microsoft takes care of everything, and everything is stored on the hard drives encrypted. (*Default*)
- **Customer-managed keys**: you create and manage the keys and provided the keys to a key vault that you reference.

## Containers

- **Containers**: a place where all of your files live.  
  - It is just like it sounds, you can put multiple file types in it, and you can also have multiple containers.  

## Access Keys and Shared Access Signature(SAS)

- **Access Keys**: authenticate your applications' requests to the storage account.
  - There are two keys you can use, so while one is being used you are able to rotate the other to constantly replace them.
  - If someone has your key, they have full access to everything on your storage account.
- **Shared Access Signature (SAS)**: is a more secure way to grant access to your blob or container.
  - Uses a URI that grants restricted access to an Azure Storage blob.
  - *Use this when you want to grant access to storage account resources for a specific time range without sharing your storage account key.*
  - The one big downside is there is no way to revoke it, the only thing you can do is regenerate the Access Key that was used in the SAS creation.

## Stored Access Policies

- **Stored Access Policy**: is a way to centrally manages SAS token settings.
  - Defined at the container level.
  - You can create only the policy (person can access from 2025/09/07 - 2025/10/07) and not actually share anything.
  - When using a Stored Access Policy you are not able to set it in the SAS creation tool.  This is better, because you can extend/shorten the time permissions without regenerating the keys.
  - Best for long lived policies >6 months.
  - Also allows you to reuse policies.

## Entra ID Access Control

- Authentication through Azure
- Shifts the authentication from what you have (secret key) to what you are.
- For StorageV2 (general purpose v2) this is enabled by default.
- Good to disable "Allow storage account key access" when using Access Control.
- This is an role assignment in IAM
- Not perfect because you do not have as fine grained control to revoke access as Access Keys.

## Lifecycle Management

**Lifecycle Management**: offers a rule-based policy for general purpose v2 and blob storage accounts.
- Allows you to transition your data to different data access tiers (more expensive -> cheaper) or delete the data at the end of their lifecycle.
- The tiers can be found in the [Blob Storage Access Tier Section](#Blob-Storage-Access-Tiers) but for summary:
  - **Move to cool storage**: for infrequently accessed data that you want to keep on cool storage for at least 30 days.
  - **Move to cold storage**: for rarely accessed data that you want to keep for at least 90 days.
  - **Move to archive storage**: use if you don't need online access and want to keep the object for 180 days or longer.
  - **Delete the blob**: deletes the object per the specified conditions.
> [!NOTE]
> The days are the **minimum** amount they will be in that storage tier that you will be charged for.

## Object Replication

**Object replication**: when enabled, blobs are copied *asynchronously* from a source storage account to a destination account.

## Storage Browser

Allows you perform some file operations such as copy/paste and more in the browser fro your storage account.  
You can also generate and SAS key to access the files right from the storage browser.  
There is also a desktop app for Windows, Mac, and Linux OSs.  

## File Shares

> [!IMPORTANT]
> Storage accounts are accessed via TCP port 445, which is the same port SMB uses.
> Many ISP's block this port by default.  So you may require a VPN in order to connect.

More similar to what you would call a file server on your own network.  
Great for a lift and shift scenario.  
Use SMB (for windows) and NFS (for Linux) protocols.  
Can utilize Azure Backup to protect file shares from accidental deletion or modification.

**Access Tiers**:
- **Transaction optimized**: lowest transaction cost pricing for transaction-heavy workloads.
  - Recommended while migrating to Azure Files.
- **Premium**: Only available for premium file storage accounts.
- **Hot**: Balanced storage and transaction pricing for workloads that have a good measure of both.
- **Cool**: Most cost-efficient storage pricing for storage-intensive workloads.
