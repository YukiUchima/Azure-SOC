<link href="./style.css" rel="stylesheet"></link>

# Microsoft Entra ID (Azure Active Directory)

- Identity and Access Management
- Creating and managing user accounts with different levels of access
  - Tenant Level
  - Management Groups
  - Subscriptions
  - Resource Groups
  - Resources (Virtual Machines)

## Create users within AAD

- Tenant-Level Global Reader

        In the Users, create new user "globalreaderjohn", setting login credentials

<img src="./assets/img/activeDirectory.png" alt="active directory"/>

<img src="./assets/img/activeDirectory2.png" alt="active directory" />

    Globalreaderjohn created as a user and will set role level in the next steps

<img src="./assets/img/activeDirectory3.png" alt="active directory" />

    In the "Assigned Roles" tab, we can set globalreaderjohn's specific roles

<img src="./assets/img/activeDirectory4.png" alt="active directory" />

    Select Global reader role: "Can read everything that a Global Administrator can, but not update..."

<img src="./assets/img/activeDirectory5.png" alt="active directory" />

    Verified role has been added to the user "globalreaderjohn"

<img src="./assets/img/activeDirectory6.png" alt="active directory" />

<br>
<br>

## Create another user for subscription level

- Subscription-Level Reader

        As done previously, added new user with credentials for "subreaderjane"

<img src="./assets/img/subActiveDir.png" alt="active directory" />

        - Add "subreaderjane" to the subscriptions-level reader by adding role to Identity and Access Management

        - Selecting my subscription, in this case "Azure subscription 1"

<img src="./assets/img/subActiveDir2.png" alt="active directory" />

    Add role assignment (to jane)

<img src="./assets/img/subActiveDir3.png" alt="active directory" />

    Found the role, now will assign it to subreaderjane

<img src="./assets/img/subActiveDir4.png" alt="active directory" />
<img src="./assets/img/subActiveDir5.png" alt="active directory" />
<img src="./assets/img/subActiveDir6.png" alt="active directory" />

    Log in to Azure as subreaderjane, which has permissions to see their subscription they are assigned

    My role is set to "Reader"

<img src="./assets/img/subActiveDir7.png" alt="active directory" />

    As a test, subreaderjane is attempting to create a resource group, and is denied.

<img src="./assets/img/subActiveDir8.png" alt="active directory" />

## Create Resource Group and A Storage Account within Azure

- Create new resource group called "Permissions-Tester"
- Assign resource group-level contributor

        As before, new user is created called "rgcontributordave"

<img src="./assets/img/rgActiveDir.png" alt="active directory" />

        New resource group created called "Permissions-Tester"

<img src="./assets/img/rgActiveDir2.png" alt="active directory" />

        Again, in Identity and Access Management (IAM), add role assignment

<img src="./assets/img/rgActiveDir3.png" alt="active directory" />

<img src="./assets/img/rgActiveDir4.png" alt="active directory" />

        Assigned "contributor" role to rgcontributordave

<img src="./assets/img/rgActiveDir5.png" alt="active directory" />

<img src="./assets/img/rgActiveDir6.png" alt="active directory" />

<br>
<br>

**Created Storage with group-level permission**

    Creating Storage accounts as "rgcontributordave"

<img src="./assets/img/rgActiveDirStorage.png" alt="active directory" />

    Verified storage account created called "random12313eas"

<img src="./assets/img/rgActiveDirStorage2.png" alt="active directory" />

    With contributor role, exercised the ability to delete resource group

<img src="./assets/img/rgActiveDirStorage3.png" alt="active directory" />

<!-- ### Notes:

    Globalreaderjohn

    globalreaderjohn@japonese2021gmail.onmicrosoft.com

    Laza995949

    cyberlab123!

<br>

    subreaderjane

    subreaderjane@japonese2021gmail.onmicrosoft.com

    Dodu754946

    cyberlab123!

<br>

    rgcontributordave

    rgcontributordave@japonese2021gmail.onmicrosoft.com

    Guga982085

    cyberlab123! -->

> Next: [Azure Lab](/azureLab.md)
