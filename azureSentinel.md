<link href="./style.css" rel="stylesheet"></link>

# Azure Sentinel (Pre-hardening)

## Create Log Analytics Workspace (log aggregator)

    In Azure portal, [Log Analytics Workspaces]

<img src="./assets/img/azureSentinel.png"/>

## Setup Sentinel and connect to Log Analytics Workspace

<img src="./assets/img/azureSentinel2.png"/>

### Create geoip watchlist

    - Name/Alias: geoip
    - Source type: Local File
    - Number of lines before row: 0
    - Search Key: network

<img src="./assets/img/azureSentinel3.png"/>

<img src="./assets/img/azureSentinel4.png"/>

### Query in Log Analytics Workspace

    Query (KQL):
        _GetWatchlist("geoip")

<img src="./assets/img/azureSentinel5.png"/>

<br>
<br>
<br>
<br>

### Sentinel Workbook - BEFORE Hardening the first 24 hours

```
In MS Sentinel, add a workbook using json file to pull log information
```

<img src="./assets/img/sentinelMap.png"/>
<img src="./assets/img/sentinelMap2.png"/>

```
First map showing sources for failed linux ssh
```

<img src="./assets/img/sentinelMap3Linux.png"/>

```
Second workbook: failed MSSql authorization
```

<img src="./assets/img/sentinelMap4MSsql.png"/>

```
Third workbook: Network Security Group log of malicious actors allowed in with minimal controls
```

<img src="./assets/img/sentinelMap5nsg.png"/>

```
Fourth workbook: Windows remote login fails
```

<img src="./assets/img/sentinelMap6windowsRDP.png"/>

```
All four workbooks created to log IP address locations
```

<img src="./assets/img/sentinel7Workbooks.png"/>

> Next: [Azure Sentinel in Workspace Pt2](/azureSentinelHardening.md)
