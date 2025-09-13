# Lab 07 - Manage Azure Storage

## What This Lab Taught Me
Learning to configure and secure blob containers, plus working with Azure file shares using Storage Browser - basically how to safely store and share files in the cloud.

## Storage Concepts That Finally Made Sense
- **Storage Account vs Containers**: Storage account is like the main folder, containers are like subfolders inside it
- **Blob Types**: Understanding when to use different blob types for different file scenarios
- **Access Levels**: The difference between private, blob-level, and container-level access

## Real-World Storage Scenarios
Practiced organizing infrequently accessed data into lower-cost storage tiers - this is how companies save money on old files they rarely need.

## Security Learning
- **Shared Access Signatures (SAS)**: Created temporary links that let people access files without giving them permanent permissions
- **Access Control**: How to let some people read files while others can upload/delete
- **Network Access**: Understanding public vs private endpoints

## What Surprised Me
- **Storage Browser Tool**: Way easier than I expected for managing files - like a file explorer in the web browser
- **Access Delays**: Changes to permissions took a minute or two to actually work
- **File Share vs Blob**: File shares work more like traditional network drives, blobs are more for applications

## Practical Discoveries
- Storage accounts have a lot of configuration options I didn't expect
- Upload speeds varied depending on file size and location
- Found the monitoring/metrics section useful for seeing storage usage

## Business Context
This isn't just about storing files - it's about doing it cost-effectively and securely. Companies use blob storage for backups, file sharing with partners, and hosting website assets.

## Key Insight
Azure Storage isn't just "cloud file storage" - it's a whole ecosystem with different tools for different needs. Understanding which tool fits which scenario is the real skill.
