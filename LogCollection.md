<link href="./style.css" rel="stylesheet"></link>

# Enabling Log Collection from VM's and NetSec Groups

- Create Azure Storage Account
- Enable Flow Logs for both VM's (Windows/Linux)
- Create Data Collection Rules
- Special Data Collection including Malware Tampering

## Create Azure Storage Account

    - Storage account name: sacyberlab024

<img src="./assets/img/logCollection.png"/>

## Enable Flow logs for both Network Security Groups

- Two flow logs, 1 each for the 2 virtual VM's

<img src="./assets/img/logCollection2.png"/>

    Select the two resources by clicking "+ Select Resource"

<img src="./assets/img/logCollection3.png"/>

    Create flow log
        - Ensure region is same as before (US EAST 2)

<img src="./assets/img/logCollection4.png"/>

## Create Data Collection Rules

- Determines which log information to be forwrded to Log Analytics Workspace

        Ensured both VM's are actively running

<img src="./assets/img/logCollectionRule1.png"/>

    Add Data Collection Rules:
    - Agents
        - Data Collection Rules

<img src="./assets/img/logCollectionRule2.png"/>

    Name the rule: "dcr-all-vms"
    Platform type: all

<img src="./assets/img/logCollectionRule3.png"/>

    Add resources to include RG-Cyber-Lab group, both the linux and windows VM

<img src="./assets/img/logCollectionRule4.png"/>

    Facility LOG_AUTH set to LOG_DEBUG Level
    All others are "none"

<img src="./assets/img/logCollectionRule5.png"/>

    Set Windows Event Logs and the destination

<img src="./assets/img/logCollectionRule6.png"/>
<img src="./assets/img/logCollectionRule7.png"/>

## Configure Special Windows Event Data Collection (Defender and Windows Firewall)

<!--
Link source:
https://github.com/joshmadakor1/Cyber-Course-v2/blob/main/Special-Windows-Event-Data-Collection-Rules/Rules.txt


Windows Defender Malware Detection XPath Query
Microsoft-Windows-Windows Defender/Operational!*[System[(EventID=1116 or EventID=1117)]]

Windows Firewall Tampering Detection XPath Query

Microsoft-Windows-Windows Firewall With Advanced Security/Firewall!*[System[(EventID=2003)]]

-->

    Select Custom and add XPATH queries
    - Malware detection XPATH
    - Malware Tampering Detection XPath

<img src="./assets/img/logCollectionRule8.png"/>

    Confirm Connection is completed for logging in Agents

    - If VM not connected, then manually force

<img src="./assets/img/logCollectionRule9.png"/>

    Query log analytics for the following:
        Syslog (linux)
        SecurityEvent (Windows)
        AzureNetworkAnalytics_CL (NSG's)

<img src="./assets/img/logCollectionRule10.png"/>
<img src="./assets/img/logCollectionRule11.png"/>
<img src="./assets/img/logCollectionRule12.png"/>

<br>
<br>
<br>
<br>

## Tenant-Level Monitoring/Logging

- Keep track of sign-in activity
- Audit trail of changes made in Azure AD for particular tenant

### Azure Active Directory Logging (in progress)

- Microsoft Entra ID

```
Create and configure collection of Audit and SignIn logs

Diagnostic setting name set to "ds-audit-signIn"
```

<img src="./assets/img/MSentraID.png"/>
<img src="./assets/img/MSentraID2.png"/>

        Verified Log Tables exist

<img src="./assets/img/MSentraID3.png"/>

        Although no results populates in query, table exists

<img src="./assets/img/MSentraID4.png"/>

<br>
<br>
<br>

### Show Logs in MS Entra ID (Azure Active Directory)

- Create new dummer user
- Sign in with dummy user
- Assign role of Global Administrator
- Delete dummy_user
- Observe Audit logs in Log Analytics Workspace of previous actions

<img src="./assets/img/MSentraID5.png"/>
<img src="./assets/img/MSentraID6.png"/>

### KQL querying when Global Administrator has been initiated

        Note: "project" is limiting the columns to specific headers to be displayed to reduce noise of unnecessary information

```

AuditLogs
| where OperationName like "add member to role" and Result like "success"
| where TargetResources[0].modifiedProperties[1].newValue like "Global Administrator" or TargetResources[0].modifiedProperties[1].newValue like "company administrator"
| order by TimeGenerated desc
| project TimeGenerated, OperationName, AssignedRole = TargetResources[0].modifiedProperties[1].newValue, Status = Result

```

<img src="./assets/img/MSentraID7.png"/>

### Attacker - generate logs simulating brute force attacks

- New user "attack-user"
- Simulate attempts to log in through azure directory

<img src="./assets/img/MSentraID8.png"/>

<br>
<br>
<br>
<br>

## Subsrciption-Level Monitoring/Logging (Activity Log)

- Enabling activity log, including logs for:

  - changing RG
  - creating RG
  - deleting RG

```
From Azure portal, open "Monitor"
Open "Activity Log" then "Export Activity Logs"
```

<img src="./assets/img/subscriptionLevel.png"/>

```
Add new diagnostic settings
```

<img src="./assets/img/subscriptionLevel2.png"/>

```
Confirmed new settings are added for AzureActivity logs
```

<img src="./assets/img/subscriptionLevel3.png"/>

### Creating new resource groups

- "Scratch-Resource-Group"
- "Critical-Infrastructure-Wastewater"

<img src="./assets/img/subscriptionLevel4.png"/>

```
Verified in AzureActivity, logs are created for creationg of groups
Next, deleting previous groups created
```

<img src="./assets/img/subscriptionLevel5.png"/>

```
Both subscriptions have been successfully deleted with logs below indicating when they were created

```

<img src="./assets/img/subscriptionLevel6.png"/>

<br>
<br>
<br>
<br>

## Resource-Level Logging (Diagnostic Setting)

- Enabling Resource-level (Data-Plane) logging into Log Analytics Workspace for:
  - Storage
  - Key Vault

### Storage Accounts Logging

```
Configure Logging for Azure Storage
    Storage Accounts
        Diagnostic Settings Configuration
            Blob -> Essentially uploading files (txt)


```

<img src="./assets/img/dataPlane.png"/>
<img src="./assets/img/dataPlane2.png"/>

```
Test blob text file
    - Storage Account
        - Containers (inside storage account)
            - New Container ("test")
                - Upload text file that was created

```

<img src="./assets/img/dataPlane3.png"/>

```
Upload blob sample text file to be logged
```

<img src="./assets/img/dataPlane4.png"/>

#### Review Blob Collections Data in Log Analytics

<img src="./assets/img/dataPlane5.png"/>

- Table name is "StorageBlobLogs"
- Queried and found log of when file was uploaded

<img src="./assets/img/dataPlane6.png"/>

```
Deleting blob container, and then observing log of deletion
```

<img src="./assets/img/dataPlane6.png"/>
<img src="./assets/img/dataPlane7.png"/>
<img src="./assets/img/dataPlane8.png"/>

### Creating Key Vault and Logging it

- Create Key Vault
- Create Secret to store in Key Vault
- Log secret to Analytics Workspace when users access it

<img src="./assets/img/keyVault2.png">

<img src="./assets/img/keyVault.png"/>

```
Create key vault

```

<img src="./assets/img/keyVault3.png"/>

```
Stored secret inside key vault
```

<img src="./assets/img/keyVault4.png"/>

```
Setting up diagnostics settings for secret to be logged
    - From inside Key Vaults, go to Diagnostic Settings to create a new setting
```

<img src="./assets/img/keyVault6.png"/>

#### Observing Key Vault Logs

```
Key Vault Test Logs
// List out Secrets
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.KEYVAULT"
| where OperationName == "SecretList"

// Attempt to view passwords that don't exist
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.KEYVAULT"
| where OperationName == "SecretGet"
| where ResultSignature == "Not Found"

// Viewing an actual existing password
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.KEYVAULT"
| where OperationName == "SecretGet"
| where ResultSignature == "OK"

// Viewing a specific existing password
let CRITICAL_PASSWORD_NAME = "Tenant-Global-Admin-Password";
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.KEYVAULT"
| where OperationName == "SecretGet"
| where id_s contains CRITICAL_PASSWORD_NAME

// Updating a password Success
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.KEYVAULT"
| where OperationName == "SecretSet"

// Updating a specific existing password Success
let CRITICAL_PASSWORD_NAME = "Tenant-Global-Admin-Password";
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.KEYVAULT"
| where OperationName == "SecretSet"
| where id_s endswith CRITICAL_PASSWORD_NAME
| where TimeGenerated > ago(2h)

// Failed access attempts
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.KEYVAULT"
| where ResultSignature == "Unauthorized" -->

```
