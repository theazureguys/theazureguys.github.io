---
title: Updating a Basic Public IP to a Standard IP Using a Bash Script
date: 2025-07-05 12:00:00 +/-TTTT
categories: [Azure, PublicIP, Standard, Basic]
tags: [azure, basic, to, standard, public, ip, migartion, cli, bash, linux]     # TAG names should always be lowercase
---

Microsoft has announced that Basic Public IP addresses will be <a href="https://www.theazureguys.co.uk/posts/basic-ips/" target="_blank">retired soon.</a>

Microsoft provides a migration script, but I made some enhancements not included in the <a href="https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/public-ip-upgrade?tabs=azurecli#upgrade-public-ip-address" target="_blank">official version</a> that are necessary for the update to work properly. My script focuses on a single VM rather than performing a mass update across an entire subscription. Because this is a one-off task, it includes some user interaction.

## Pre-requisites

A Linux environment.
Azure CLI. a href="https://learn.microsoft.com/en-us/cli/azure/get-started-with-azure-cli?view=azure-cli-latest#install-or-run-in-azure-cloud-shell" target="_blank">Installation steps</a>

## Script

Copy the code below and save it in your preferred Linux editor (I prefer vim).

```
#!/bin/bash

echo "What is the subscriptionID?"
read SUB

echo "What is the vm name?"
read VMNAME

echo "What is the vm resource group?"
read RG

az account set --subscription $SUB

VM=$(az vm show -n $VMNAME -g $RG --query id -o tsv)
NIC=$(az vm show -n $VMNAME -g $RG --query networkProfile.networkInterfaces[0].id -o tsv)
NICRG=$(az network nic show --ids $NIC --query resourceGroup -o tsv)
NICNAME=$(az network nic show --ids $NIC --query name -o tsv)
PIP=$(az network nic show --ids $NIC --query ipConfigurations[0].publicIPAddress.id -o tsv)
PIPNAME=$(az network public-ip show --ids $PIP --query name -o tsv)
PIPRG=$(az network public-ip show --ids $PIP --query resourceGroup -o tsv)
IPCONFIG=$(az network nic show --ids $NIC --query ipConfigurations[0].name -o tsv) 

#Check if IP is set to static
if az network public-ip show --ids $PIP --query publicIPAllocationMethod | grep  Dynamic
 then az network public-ip update --allocation-method Static --ids $PIP
 
 else echo "IP Allocation confirmed to be static"
fi

#Remove Public IP from Network Card
az network nic ip-config update --public-ip-address null --nic-name $NICNAME --name $IPCONFIG -g $NICRG
#Update Public IP
az network public-ip update --ids $PIP --sku Standard
#Add Public IP address back to Network Card
az network nic ip-config update --public-ip-address "$PIPNAME" --nic-name $NICNAME --name $IPCONFIG -g $NICRG
```

Before running the script, sign in to your Azure tenant:

az login

Once saved, make it executable and run it:

vim UpdatePublicIP.sh (copy the code into this file)

chmod +x UpdatePublicIP.sh

./UpdatePublicIP.sh
