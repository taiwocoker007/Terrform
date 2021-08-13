# Single Region Base Lab Environment for Azure

## Overview
This code creates a simple Lab environment within a Single Azure Region. The idea here is that it allows for quick deployment of VNETs, Subnets, and a Domain Controller to simulate smaller environments or provide a quick lab for any test requirements.

*It is not intended for production use!*

## Actions
The following resources are deployed:

1. Two Resource Groups, one for the Lab infrastructure, and another for Security related items.
2. Two VNETs, a Hub and a Spoke, which are peered. DNS is set on the VNETs to the Domain Controller IP, Azure DNS, and finally, Google DNS. 
3. Three Subnets in each VNET, with a Subnet delegated to Azure NetApp Files in the Spoke VNET. 
4. Uses the Automatic-ClientIP-NSG to setup a Network Security Group that allows RDP access in - this NSG rule uses the external IP of the machine that runs Terraform. 
5. Associates the created NSG to all Lab Subnets.
6. Creates a Key Vault with a randomised name, using Azure-KeyVault-with-Secret, and then creates a password as a Secret within the Key Vault that is used later to setup a VM.
7. Creates a Public IP for the Domain Controller VM.
8. Creates a Network Interface Card and associates the above Public IP. 
9. Creates a Data Disk for NTDS Storage on the Domain Controller VM.
10. Creates a Windows 2019 VM to act as a Domain Controller. The Username for this VM is a Variable, and the Password is saved as a Secret in the Key Vault. (It was automatically generated in Step 6).
11. Attaches the Data Disk created in step 9, with caching Turned off. 

### Note this is a cut down version of the Single Region BaseLab as this repo is for a lab day session!
