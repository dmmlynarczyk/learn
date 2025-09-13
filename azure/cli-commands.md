# CLI Commands For AZ-104 Exam

The exam does not require programming in the sense of coding, but does require knowledge of scripting (PowerShell, Azure Portal, and Bash/CLI).  
Additionally it is good to know how to at least read JSON templates and CLI responses.

## Why Do We Need This?

- Allows for automation of commonly used tasks.
- Allows for error reduction, since you can now check scripts into a source control repository and copy known good working scripts.
  - Now all you need to do is edit minimal things like names or IP addresses and run them.
  - Also allows you to share and track changes to scripts.

## Memorizing PowerShell and CLI Commands

There is a predictable naming convention for commands.  
**For Bash commands**:  
``` bash
az vm list
az vm create
az vm delete
```
``` bash
az keyvault list
az keyvault create
az keyvault delete
```
Notice the convention that the middle word defines the service or subservice that we will be running commands on.  
**For PowerShell commands**:  
``` powershell
Get-AzVM
New-AzVM
Remove-AzVM
```
Verb is the first part of the word but the last bit is the consistent service name, *but with no spaces like in Bash.*  

## Important PowerShell Commands

- **To install a new AZ module in PowerShell** run the following command as an administrator:  
  ``` powershell
  Install-Module -Name AZ -AllowClobber -Repository PSGallery -Force
  ```
- **To update a new AZ Module** run the following command as an administrator:
  ``` powershell
  Update-Module -Name AZ -AllowClobber -Repository PSGallery
  ```
- **To connect to an Azure account**:
  ``` powershell
  Connect-AzAccount
  ```
  - *This will bring up a sign-in screen for you to authenticate from.*
- **To download the latest version of PowerShell**:
  - Download for your operating system from [Github](https://github.com/PowerShell/PowerShell/releases)

## EntraID Management

### Creating A New User

The following two lines will take a password, that you make that is complex enough to meet your organizations complexity requirements and assign it to a variable `$passwordProfile`.  
Next it will create a new user with specific flags such as UserPrincipalName, DisplayName, Password, AccountEnabled, JobTitle, Department, and UsageLocation.  

1. Assign your variables:
   ``` powershell
   $password = <string>
   $uname = <string>
   $nickname = <string>
   $upn = <string> # this is the email address
   $jobTitle = <string>
   $dept = <string>
   $location = <string>
   ```

2. Store your complex password:
   ``` powershell
   $passwordProfile = New-Object -TypeName "Microsoft.Azure.PowerShell.Cmdlets.Resources.MSGraph.Models.ApiV10.MicrosoftGraphPasswordProfile" -Property @{Password=$password}
   ```
3. Create a new user for your domain:
   ``` powershell
   New-AzADUser -UserPrincipalName $upn -DisplayName $uname -MailNickname $nickname -PasswordProfile $passwordProfile -AccountEnabled $true -JobTitle $jobTitle -Department $dept -UsageLocation $location
   ```

The flags used for creating the user come from [learn.microsoft.com](https://learn.microsoft.com/en-us/powershell/module/az.resources/new-azaduser?view=azps-14.3.0)

### Creating An External User

The following will create a new external user with appropriate flags filled out.

1. Assign the variables:
   ``` powershell 
   $emailAddress = <string>
   $displayName = <string>
   $customizedMessageBody = <string>
   ```
2. Create a new external user for your domain:
   ``` powershell  
   $invitation = New-AzureADMSInvitation -InvitedUserDisplayName $displayName -SendInvitationMessage $True -InvitedUserEmailAddress $emailAddress -InviteRedirectUrl "https://account.activedirectory.windowsazure.com/" -InvitedUserMessageInfo @{ "MessageLanguage" = "en-US"; "CustomizedMessageBody" = $customizedMessageBody } -InvitedUserType Guest
   ```
The flags used for creating the user come from [learn.microsoft.com](https://learn.microsoft.com/en-us/powershell/module/azuread/new-azureadmsinvitation?view=azureadps-2.0)

### Creating A Security Group

The following will create a security group with mail disabled.

1. Assign the variables:
   ``` powershell
   $description = <string>
   $displayName = <string>
   $mailNickname = <string>
   ```
2. Create the group:
   ``` powershell
   New-AzureADMSGroup -DisplayName $displayName -Description $description -MailEnabled $False -MailNickname $mailNickname -SecurityEnabled $True 
   ```
The flags used for creating the user come from [learn.microsoft.com](https://learn.microsoft.com/en-us/powershell/module/azuread/new-azureadmsgroup?view=azureadps-2.0)
For bulk actions I found [THIS](https://www.linkedin.com/pulse/creating-groups-azure-ad-using-powershell-ewan-monro/?articleId=6506786193370423296) article on Linkedin.

### Add Multiple Users To A Group

The following will grab the group you specify and add multiple users to it:

1. Get the group you are looking for with:
   ``` powershell
   Get-AzADGroup
   ```
2. Assign your specific group ID to a variable
   ``` powershell
   $group = Get-AzADGroup -DisplayName "IT Lab Administrators"
   $groupId = $group.Id
   ```
3. Add your list of users to a variable:
   ``` powershell
   $users = @("externalUserEmail", "internalUserEmail")
   ```
4. Add your users to the group and confirm they were added:
   ``` powershell
   foreach ($user in $users) {
    Add-AzADGroupMember -TargetGroupObjectId $groupId -MemberUserPrincipalName $user
    Write-Host "Added $user to It Lab Administrators group"
   }
   ```
The flags used for creating the user come from [learn.microsoft.com](https://learn.microsoft.com/en-us/powershell/module/az.resources/add-azadgroupmember?view=azps-14.4.0)

## Resource Group Management

### Create A Resource Group

``` powershell
New-AzResourceGroupDeployment -ResourceGroupName "resourceGroupName" -TemplateFile "template.json" -TemplateParameterFile "parameters.json"
```

### Delete A Resource Group

**PowerShell**
``` powershell
Remove-AzResourceGroup -Name resourceGroupName
```

**Bash**
``` bash
az group delete --name resourceGroupName
```

## Compute Resource Management

### Create A VMSS

``` bash
az vmss scale --name azvmssdemo --resource-group resourceGroupName --new-capacity 2
```

### Create a VM (BASIC) 

*This is the most basic way to create a VM, it will get defaults for all values.*

``` powershell
New-AzVM -Name <name> -Credential (Get-Credential)
```

### Create a VM (ADVANCED)

**PowerShell**
``` powershell
New-AzVm -ResourceGroupName 'az104-rg8' -Name 'myPSVM' -Location 'East US' -Image 'Win2019Datacenter' -Zone '1' -Size 'Standard_D2s_v3' -Credential (Get-Credential)
```

**Bash**
``` bash
az vm create --name myCLIVM --resource-group az104-rg8 --image Ubuntu2204 --admin-username localadmin --generate-ssh-keys
```

### List VMs In A Specific Resource Group

**PowerShell**
``` powershell
Get-AzVM -ResourceGroupName 'az104-rg8' -Status
```

**Bash**
``` bash
az vm show --name  myCLIVM --resource-group az104-rg8 --show-details
```

### Deallocate (Stop) A VM

**PowerShell**
``` powershell
Stop-AzVM -ResourceGroupName 'az104-rg8' -Name 'myPSVM' 
```

**Bash**
``` bash
az vm deallocate --resource-group az104-rg8 --name myCLIVM
```