<link href="./style.css" rel="stylesheet"></link>

# AZURE

## Virtual Machines

    Created Virtual Labs
        - Windows-vm
        - Linux-vm

![VM](./assets/img/CreateVMS.png)

## Set Network Security Groups (Allow all traffic)

    Windows Virtual Environment

![Windows Traffic](./assets/img/NSG1.png)
Updated Security Group to allow all traffic
![Windows Traffic](./assets/img/NSG2.png)

<br>
<br>

    Linux Virtual Environment

![Windows Traffic](./assets/img/NSG3.png)
Updated Security Group to allow all traffic in
![Windows Traffic](./assets/img/NSG4.png)

<br>
<br>

## Remote Access Virtual Machines

![](./assets/img/RDP1.png)

## Disable Firewalls

![](./assets/img/RDP2.png)
![](./assets/img/FirewallDisabled.png)
![](./assets/img/FirewallDisabled2.png)
![](./assets/img/FirewallDisabled3.png)

## Install Database (SQL Server Evaluation)

![](./assets/img/SQL1.png)
![](./assets/img/SQL2.png)

## Install SSMS (SQL Server Management Studio)

![](./assets/img/SSMS.png)

    Enabling logging for SQL Server to be ported into Windows Event Viewer

![](./assets/img/regeditNetServ.png)

## Configure the audit object access setting in Windows using auditpol

```
auditpol /set /subcategory:"application generated" /success:enable /failure:enable
```

## Linux SSH

![](./assets/img/linuxPing.png)
![](./assets/img/linuxPing2.png)

## Azure: Logging and SecOps

**Creating another VM to attack linux and windows VM**

![](./assets/img/attacker.png)
![](./assets/img/attacker2.png)

    Remote connect to attack-vm

![](./assets/img/attack3.png)

### From Attack-VM, attempt login to Windows-VM

![](./assets/img/rdpAttack.png)
![](./assets/img/rdpAttack2.png)

    Attempting to login to Windows-VM SSMS database from Attack-VM

![](./assets/img/rdpAttack3.png)
![](./assets/img/rdpAttack4.png)
![](./assets/img/rdpAttack5.png)

### From Attack-VM, attempting login to Linux-VM

![](./assets/img/linxAttack.png)
![](./assets/img/linxAttack2.png)
![](./assets/img/linxAttack3.png)
![](./assets/img/linxAttack4.png)

### Review event logger of previous attempts to log ins (Brute Force)

![](./assets/img/attackEvents.png)
![](./assets/img/attackEvents2.png)
![](./assets/img/attackEvents3.png)
![](./assets/img/attackEvents4.png)
![](./assets/img/attackEvents5.png)

### Logs in Linux

![](./assets/img/attackEventsLX.png)
![](./assets/img/attackEventsLX2.png)
![](./assets/img/attackEventsLX3.png)
![](./assets/img/attackEventsLX4.png)
