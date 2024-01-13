<link href="./style.css" rel="stylesheet"></link>

# Securing Cloud

    1. Inspect MDC Secure Score
    2. Inspect MDC Recommendations
    3. Enable MDC Regulatory Compliance
        - NIST 800-53 (Security and Privacy Controls)

### Microsoft Defender For Cloud Secure Score

    Current Score at 50%

<img src="./assets/img/MDC1.png" />

### MDC Recommendations

    Reviewing Recommendations

<img src="./assets/img/MDC2.png" />

<br>
<br>

### MDC Regulatory Compliance Enabled

    In regulatory compliance, proceed to manage compliance policies

<img src="./assets/img/MDC3.png" />

    Inside Azure Subscription, proceed to security policies and search for 800-53

<img src="./assets/img/MDC4.png" />
<img src="./assets/img/MDC5.png" />

    Enable NIST 800-53 security policy

<img src="./assets/img/MDC6.png" />

    Confirmed NIST 800-53 has been applied

<img src="./assets/img/MDCnist.png" />

<br>
<br>
<br>
<br>

### Securing key vault with private endpoint connection

- Creating private endpoint will result to private address when accessing from VM (IP: 10.0.0.#)
- This is more secure since it can only be accessed with same virtual network and not from the public

<br>

    With the key vault, proceed to networking and disable public access

<img src="./assets/img/MDCnistKeyVault.png" />

    In Private Endpoint Connections tabe, create a new private endpoint "PE-AKV"

<img src="./assets/img/MDCnistKeyVault1.png" />

    Fill information corresponding to subscription and resource group

<img src="./assets/img/MDCnistKeyVault2.png" />
<img src="./assets/img/MDCnistKeyVault3.png" />
<img src="./assets/img/MDCnistKeyVault4.png" />
<img src="./assets/img/MDCnistKeyVault5.png" />

<br>
<br>
<br>
<br>

### Securing Blob storage with private endpoint connection

- Similar to previous securing of key vault, create private endpoint to the storage in the resource group

<br>

    In storage accounts, procced to disable public network access in the networking tab

<img src="./assets/img/MDCstorage.png" />

    Proceed to create a private endpoint for the storage account

<img src="./assets/img/MDCstorage1.png" />
<img src="./assets/img/MDCstorage2.png" />
<img src="./assets/img/MDCstorage3.png" />
<img src="./assets/img/MDCstorage4.png" />
<img src="./assets/img/MDCstorage5.png" />
<img src="./assets/img/MDCstorage6.png" />

### Verify endpoints are created in topology

    Inside Network Watcher, select topology and filter scope to corresponding resource group and locations

    Resource Group: RG-Cyber-Lab
    Locations: East US 2

<img src="./assets/img/MDCnetworkWatcher.png" />

<br>
<br>
<br>
<br>

### Creating subnet on virtual network

    Add new network security group for subnet

<img src="./assets/img/MDCnsg.png" />

    In the appropriate virtual network, Lab-VNet for this instance, add new subnet (nsg-subnet)

<img src="./assets/img/MDCnsg1.png" />

    Inside network watcher topology, observe subnet has been added and ready to be configured

<img src="./assets/img/MDCnsg2.png" />
