## Azure PowerShell

Install Azure Powershell Module:
	 `Install-Module -Name Az -AllowClobber -SkipPublisherCheck `
	 `Install-Module -Name AzureAD`
	 
Import Azure cmdlets
	`Import-Module Az`

Connect to your account:
	`Connect-AzAccount`

List available tenants:
	`Get-AzTenant`
Select context:
	`Select-AzContext "604c1504-c6a3-4080-81aa-b33091104187 - Francisco.Varela@healthineersm365.com"`
	
Get active subscription:
	`Get-AzContext`

Get resource groups:
	`Get-AzResourceGroup | Format-Table` 

Create resource group
	`New-AzResourceGroup -Name <name> -Location <location>`

Create a virtual machine:
	Ref:[Exercise - Create an Azure Resource using scripts in Azure PowerShell - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/automate-azure-tasks-with-powershell/6-exercise-create-resource-interactively)
	New-AzVm -ResourceGroupName learn-a9337ed2-418d-480e-beb8-6d5b37d255df -Name "testvm-eus-01" -Credential (Get-Credential) -Location "East US" -Image Canonical:0001-com-ubuntu-server-focal:20_04-lts:latest -OpenPorts 22 -PublicIpAddressName "testvm-01"

Stop a virtual machine:
	Stop-AzVM -Name $vm.Name -ResourceGroupName $vm.ResourceGroupName

