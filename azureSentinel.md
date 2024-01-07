<link href="./style.css" rel="stylesheet"></link>

# Azure Sentinel

## Create Log Analytics Workspace (log aggregator)

    In Azure portal, [Log Analytics Workspaces]

<img src="./assets/img/azureSentinel.png"/>

## Setup Sentinel and connect to Log Analytics Workspace

<img src="./assets/img/azureSentinel2.png"/>

## Create geoip watchlist

    - Name/Alias: geoip
    - Source type: Local File
    - Number of lines before row: 0
    - Search Key: network

<img src="./assets/img/azureSentinel3.png"/>

<img src="./assets/img/azureSentinel4.png"/>

## Query in Log Analytics Workspace

    Query (KQL):
        _GetWatchlist("geoip")

<img src="./assets/img/azureSentinel5.png"/>
