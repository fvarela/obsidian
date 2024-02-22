# C1 Manage resources in Azure

True or False? Cloud computing is simply a datacenter available through the internet.
	True
	X False

What are the three deployment cloud computing models available? Select all options that apply.
	Governmental
	X Private
	X Hybrid
	Enterprise
	X Public
	
What are some reasons to use the public cloud model? Select all options that apply.
	X Hardware maintenance
	X Service consumption through on-demand or subscription model
	X Geographic dispersity
	Automation
	Up-front investment of hardware

What are some reasons to use the private cloud model? Select all options that apply.
	X Data sovereignty and security
	No pre-existing environment
	X Regulatory compliance
	X Legacy apps

What are the three cloud service models? Select all options that apply.
	X Infrastructure-as-a-service (IaaS)
	X Software as a service (SaaS)
	Cloud-as-a-service (CaaS)
	X Platform as a service (PaaS)

If you want to have control over the apps, data, run-time, middleware and OS, which service model should you choose?
	X IaaS
	PaaS
	SaaS

True or false? The Azure CLI runs on Linux and Windows only.
	True
	X False

If you want to restart a virtual machine (VM) using the Azure CLI, which command should you use?
	az restart – n MyVm
	X az vm restart -g MyResourceGroup -n MyVm
	vm restart -g MyResourceGroup -n MyVm
	vm restart -name MyVM

When you’re working with the Azure CLI in the Bash environment, if you want to assign a variable, which command syntax should enable you to do that?
	- $variable="value"
	- String variable = “value”
	- variable = “value”
	X variable="value"

If you want to search for a particular command in the Azure CLI related to blob for example, what command should help you?
	az list blob
	X az find blob
	az get blob
	az show blob

When using the Azure CLI, if you want to create a resource group, which command should help you complete that?
	az create resourcegroup --name MyResGroup --location “West US”
	az group create --name myresgroup --location westus
	X az group create --name MyResGroup --location “West US”
	X az create group --name myresgroup --location westus

Business has a new short-term project that requires a SQL Server database. The IT department does not have available hardware that can meet the performance requirements or even the resources to deploy it. The project starts next week. The database will no longer be required after the project is over. Which cloud service model would be suitable for this scenario?
	SaaS
	X PaaS
	IaaS

You deployed six virtual machines in the cloud. The VMs are connected together in a virtual network. The VMs have access to x-ray image files in cloud storage. One of the virtual machines is a web server that hosts a website exposed to the internet for patients to access their records. There is a VPN that connects the solution to your on-premises datacenter for patient information to display with the image files. Which cloud service model would be suitable for this scenario?
	PaaS
	X IaaS
	SaaS

The start-up company you work for has a small number of employees who need to collaborate. They need email, calendar scheduling, and a place to store business documents. The team is somewhat technical but do not have the time or hardware to implement and manage a solution. Which cloud service model would be suitable for this scenario?
	IaaS
	X SaaS
	PaaS

If you want to verify the creation or view a detailed list for a set of resources, virtual machines for example, which Azure CLI command should you use?
	az vm reveal
	az getlist vm
	X az vm list
	az showlist vm

What if you want to retrieve a more concise view, like a table of the VM’s on your subscription? Which Azure CLI command should you use?
	az vm list –output
	az vm list --table output
	X az vm list --output table
	az vm list –table

Let’s suppose you’ve already declared a few variables in the Azure CLI, such as $AZURE_WEB_APP for the name of the web app, $RESOURCE_GROUP for the resource group and $AZURE_APP_PLAN for the app service plan. You would now like to create the web app using the Azure CLI. Which command is the right one?
	X az webapp create --name $AZURE_WEB_APP --resource-group $RESOURCE_GROUP --plan $AZURE_APP_PLAN
	az init webapp --name $AZURE_WEB_APP --resource-group $RESOURCE_GROUP --plan $AZURE_APP_PLAN
	az webapp deploy --name $AZURE_WEB_APP --resource-group $RESOURCE_GROUP --plan $AZURE_APP_PLAN

If you want to test the web app you created is up and running, which Azure CLI command should you run to see the “Quickstart” page created by Azure?
	X curl $AZURE_WEB_APP.azurewebsites.net
	get $AZURE_WEB_APP.azurewebsites.net
	show $AZURE_WEB_APP.azurewebsites.net
	list $AZURE_WEB_APP.azurewebsites.net

Let’s imagine you need to create App Service Plans for different environments of testing (unit, integration, acceptance) as a one-off task. Which administrative tool would be suitable to do this?
	Azure CLI
	Azure PowerShell
	X Azure Portal

What if you are tasked with creating multiple VMs for testing, likely several times each week. What tool should help you do the job? Select all options that apply.
	Azure Portal
	X Azure CLI
	X Azure PowerShell

Which PowerShell console allows you to write scripts? Select all options that apply.
	Windows PowerShell (x86)
	X Windows PowerShell ISE
	Windows PowerShell
	X Windows PowerShell ISE (x86)

On Windows, the Azure PowerShell module requires a PowerShell major version of 5.0 or higher. Which PS command can help you verify the current version?
	$Table.PSVersion
	$PSVersionTable
	$PSVersion.PSVersion
	X $PSVersionTable.PSVersion

X When installing the PowerShell Core on Linux, you will use the Advanced Packaging Tool and the Bash command line to perform a sequence of 5 steps. Which is the first step?
	- Install PowerShell Core.
	Start PowerShell.
	- Register the Microsoft Ubuntu repository so the package manager can locate the PowerShell Core package.
	X Import the encryption key for the Microsoft Ubuntu repository.
	- Update the list of packages.

When using PowerShell in interactive mode, you type commands known as cmdlets that execute immediately. Which statement below describes the purpose of cmdlets?
	X A cmdlet can manipulate a single feature.
	A cmdlet can accommodate an array of features at once, similar to lines of code we see in programming languages.
	A cmdlet can manipulate a maximum amount of 6 features at once.

Which is the syntax naming convention that the PowerShell cmdlets follow?
	- Noun-verb
	Noun-verb and verb
	X Verb-noun

X Which command should you run in Windows PowerShell to install the latest Az module?
	- Install-Module -Name AzModule -AllowClobber
	- Install-Module -Name AzModule
	X Install-Module -Name Az -AllowClobber -SkipPublisherCheck
	Install-Module -Name Az -SkipPublisherCheck

Depending on the security configuration of the machine you’re trying to install the Az module on, the Import-Module might fail because of a restriction on the execution policy. Which command should you run if this happens?
	- ExecutionPolicy-Set Signed
	- ExecutionPolicy-Set Allow
	- Set-ExecutionPolicy Unrestricted
	- Set-ExecutionPolicy RemoteSigned

What is the PowerShell cmdlet that you run to execute a script?
	Run-file myScript.ps1
	Execute-script myScript.ps1
	X `.\myScript.ps1` 
	Execute-file myScript.ps1

Which statement best describes a resource group?
	A group of users that have access to certain resources on Azure
	X A logical container for resources deployed on Azure
	A group of resources automatically allocated on one type of resource

True or false? One resource can be a member of several resource groups.
	True
	X False

If you no longer need all of the resources in one resource group, which is the easiest way to dispose of them?
	Delete the resources one by one
	Create a script in Azure PowerShell that deletes the resources
	X Delete the entire resource group

If you want to block a certain size of a VM from deploying in an environment, what should you implement?
	X Policies
	RBAC
	Tags
	Resource locks

What is the limit of tags a resource can have?
	12
	24
	40
	X 50

Which one of these resource types can't be moved between resource groups?
	X Azure Active Directory Domain Services
	Azure Storage accounts
	Azure virtual machines

Which one of these resource types can be moved across resource groups?
	Azure Backup vault
	Azure Application Gateway
	X Azure virtual networks

When can you move a virtual machine?
	You can move virtual machines, but you have to first remove any network security groups.
	X You can move virtual machines, but you have to first make sure that you can move all of its dependent resources along with it.
	You can move virtual machines, but you have to first make sure that you can remove any SSD disks before attempting to move them.

True or false? You cannot move a resource from a resource group to another resource group in a different subscription.
	True
	X False

You identified that a production VM has been deployed in a development resource group. You want to make sure that VM is not in danger of being compromised. What should you do?
	Put a Delete resource lock on it
	Assign a “environment:production” tag on it
	Delete the resource and redeploy it on the production resource group
	X move the resource into the production resource group (on which access is limited and controlled)
 
Some resources can be moved between resource groups, while other cannot. From the list below, which can be moved? Select all options that apply.
	Azure App Service gateways
	X Azure Storage accounts
	Azure Active Directory domain services
	X Azure virtual machines
	X Azure virtual networks
	Azure Backup vaults

When planning to move a resource, regardless of the tool you use, you must first verify whether the process will be successful by using a validation operation. Which of the tools below can you call the validate move operation from the Azure REST API to test the move? Select all options that apply.
	Azure Portal
	X Azure CLI
	X Azure PowerShell

When attempting to validate a move using the Azure REST API, what information do you need to provide? Select all options that apply.
	Current resource group region
	X Resource ID for the destination resource group
	X Name of the current resource group
	X Azure subscription ID
	X Resource ID for each of the resources in your original resource group
	X Account access token

True or false? Azure resources can be moved between resource groups without limitations.
	True
	X False

X Let’s say you want to add the “Department=Finance” resource tag to the msftlearn-vnet1 virtual network using the Azure CLI. Which command should execute the job?

	X az resource tag --tags Department=Finance \
	
	--resource-group msftlearn-core-infrastructure-rg \
	
	--name msftlearn-vnet1 \
	
	--resource-type "Microsoft.Network/virtualNetworks"
	
	az resource tag --tags Department=Finance \
	
	--resource-group msftlearn-core-infrastructure-rg \
	
	--resource-type "Microsoft.Network/virtualNetworks"
	
	az tag --tags Department=Finance \
	
	--resource-group msftlearn-core-infrastructure-rg \
	
	--name msftlearn-vnet1 \
	
	--resource-type "Microsoft.Network/virtualNetworks"
	
	az resource tag --tags Department=Finance \
	
	--resource-group msftlearn-core-infrastructure-rg \
	
	--name msftlearn-vnet1 \
	
	--resource-type "Microsoft.Network”


X Tagging your resources can provide benefits in various aspects of your resource administration. Which are some of the aspects that tags can bring value to? Select all options that apply.
	X Billing
	X Automation
	Authentication
	RBAC
	X Monitoring
	X Retrieving resources

Creating and assigning a policy to a resource group helps with enforcing some best practice standards or organizational standards. Which are some of the aspects that can be enforced by applying policies? Select all options that apply.
	2-factor authentication
	Read/Write access
	X Types of resources to be created
	X Tag assignment
	X Resource location
	X Naming conventions

Making use of role-based access control (RBAC) enables you to secure what can be done with your resources and by who. Which of the following features are not possible through RBAC?
	- Grant users the lowest privilege required to perform tasks
	X Restrict certain resources from being deployed in a resource group
	- Allow an application to access some or all resources in a resource group

You have a resource group that contains business critical resources, such as a CosmosDB, a virtual network, virtual machines, and storage accounts. You want to make sure nobody can delete any of the resources in this group. Which approach would be best for this scenario?
	Apply a Read-Only lock on every resource in the group
	X Apply a Delete lock on the resource group
	Apply a Read-Only lock on the resource group
	Apply a Delete lock on every resource in the group

When submitting the GET request to the location URL to test your validation, what status code should you get for if the move will be successful?
	X 204
	- 202
	403
	500
  
You are configuring a development environment for your team. You deploy the latest Visual Studio image from the Azure Marketplace to your Azure subscription. The development environment requires several software development kits (SDKs) and third-party components to support application development across the organization. You install and customize the deployed virtual machine (VM) for your development team. The customized VM must be saved to allow provisioning of a new team member development environment. You need to save the customized VM for future provisioning. Which tools or services should you use to generalize the VM?
	Visual Studio command prompt
	Azure Migrate
	X Azure PowerShell
	Azure Backup

You have an Azure subscription named Subscription1 that contains a virtual network named VNet1. VNet1 is in a resource group named RG1. Subscription1 has a user named User1. User1 has the following roles:
**• Reader**
**• Security Admin**
**• Security Reader**
You need to ensure that User1 can assign the Reader role for VNet1 to other users. What should you do?
	X Assign User1 the Owner role for VNet1.
	Remove User1 from the Security Reader and Reader roles for Subscription1.
	Remove User1 from the Security Reader and Reader roles for Subscription1. Assign User1 the Contributor role for Subscription1.
	Assign User1 the Network Contributor role for VNet1.

You have an Azure App Services Web App, Azure SQL Database instance, Azure Storage Account, and an Azure Redis Cache instance in a resource group. A developer must be able to publish code to the web app. You must grant the developer the Contributor role to the web app. Which two commands can you use? Each correct answer presents a complete solution. Select all options that apply.
	New-AzRoleDefinition
	X New-AzRoleAssignment
	X az role assignment create
	az role definition create

You created a custom RBAC role namedCustomrole1 as shown below, and you’ve assigned it to a user named user1. What are the operations that user1 can perform? Select all options that apply.

**{**

**"Name": "Customrole1",**

**"Id": "88888888-8888-8888-8888-888888888888",**

**"IsCustom": true,**

**"Description": "Custom role one",**

**"Actions": [**

**"Microsoft.Storage/*/read",**

**"Microsoft.Network/*/read",**

**"Microsoft.Compute/*/read",**

**"Microsoft.Compute/virtualMachines/start/action",**

**"Microsoft.Compute/virtualMachines/restart/action",**

**"Microsoft.Authorization/*/read",**

**"Microsoft.ResourceHealth/availabilityStatuses/read",**

**"Microsoft.Resources/subscriptions/resourceGroups/read",**

**"Microsoft.Insights/alertRules/*",**

**"Microsoft.Insights/diagnosticSettings/*",**

**"Microsoft.Support/*"**

**],**

**"NotActions": [],**

**"DataActions": [],**

**"NotDataActions": [],**

**"AssignableScopes": [**

**"/subscriptions/{subscriptionId1}",**

**"/subscriptions/{subscriptionId2}",**

**"/providers/Microsoft.Management/managementGroups/{groupId1}"**

**]**

}
	Create virtual machine
	Create storage accounts
	X Monitor virtual machines
	X Start virtual machine
	X Restart virtual machine

You have an Azure subscription named Subscription1. Subscription1 contains a resource group named RG1. RG1 contains resources that were deployed by using templates.You need to view the date and time when the resources were created in RG1. Solution: From the RG1 blade, you click Automation script. Does this meet the goal?
	Yes
	X No

Your company is developing a solution that allows smart refrigerators to send temperature information to a central location. You have an existing Service Bus. The solution must receive and store message until they can be processed. You managed to successfully create an Azure Service Bus Instance via CLI by providing a name, pricing tier, subscription, resource group, and location. What Azure CLI should you run next in order to complete the configuration?
	-az servicebus namespace create --resource-group fridge-rg --name fridge-ns --location fridge-loc
	X az servicebus queue create --resource-group fridge-rg --namespace-name fridge-ns --name fridge-q
	New-AzureRmResourceGroup -Name fridge-rg -Location fridge-loc

You have an Azure subscription named Subscription1 that contains a Resource Group in which multiple resource types have been created (VMs, Webapps, SQL Databases, etc).You plan on assigning an RBAC role to a user which will need to manage all the operational aspects of these resources and will also have the ability to assign roles to other users on these resources. What role should you assign to this user?
	X Owner
	Contributor
	Reader
	Security Administrator

You have deployed a VM named “myVM” in a Resource Group named “myResourceGroup”.You realized that you need to scale the VM to a “Standard_DS3_v2” size and you plan on doing this via PowerShell.Complete the following script:
$vm = Get-AzVM -Name MyVM -ResourceGroupName MyResourceGroup
**[…]**
Update-AzVM -ResourceGroupName MyResourceGroup -VM $vm**
	$vm = “Standard_DS3_v2”
	X $vm.HardwareProfile.vmSize = “Standard_DS3_v2”
	$vm.Size = “Standard_DS3_v2”

You have deployed a VM named “MyVM” in a Resource Group named “myResourceGroup”.
The VM is currently stopped. You plan on starting this VM.
Which PowerShell command(s) should you run to perform this action?
	Restore-AzVm -Name MyVM -ResourceGroupName “myResourceGroup”
	Stop-AzVm -Name MyVM -ResourceGroupName “myResourceGroup”
	X Start-AzVm -Name MyVM -ResourceGroupName “myResourceGroup”

You have an Azure Subscription in which it is deployed an App Service Plan named “myASP” inside a Resource Group name “myResourceGroup”. The App Service Plan currently runs on a B1 SKU.
You plan on scaling the App Service Plan to an S2 SKU.
Which command(s) should you run to perform this action?
	az appservice plan change –name “myWebapp” --resource-group “myResourceGroup” --sku S2
	- az appservice plan update --name “myASP” --resource-group “myResourceGroup” --plan S2
	az appservice plan update --name “myASP” --resource-group “myResourceGroup” --sku S2


**You are creating a virtual machine in an Azure subscription named Subscription1 using PowerShell. Which two parameters should you add to complete below command?**
Select all options that apply. 
New-AzVm -Name "myVM" -Location "East US" -SubnetName "mySubnet" -SecurityGroupName "myNetworkSecurityGroup" -PublicIpAddressName "myPublicIpAddress" -OpenPorts 80,3389**
	? DiskSize 4096
	? VirtualNetworkName "myVnet"
	X ResourceGroupName "myResourceGroup"
	- OperatingSystem "win2016datacenter"

You are designing a solution to secure a company's Azure resources. The environment hosts 10 teams. Each team manages a project and has a project manager, a virtual machine (VM) operator, developers, and contractors.
Project managers must be able to manage everything except access and authentication for users. VM operators must be able to manage VMs, but not the virtual network or storage account to which they are connected. Developers and contractors must be able to manage storage accounts.
You need to provide access for Virtual Machine Operator. What role should you provide?
	Contributor
	Storage account Contributor
	Owner
	Reader
	X Virtual Machine Contributor

You are developing a solution to secure a company's Azure resources. The environment hosts 10 teams. Each team manages a project and has a project manager, a virtual machine (VM) operator, developers, and contractors. Project managers must be able to manage everything except access and authentication for users. VM operators must be able to manage VMs, but not the virtual network or storage account to which they are connected. Developers and contractors must be able to manage storage accounts. You need to provide access for Developers and Contractors. What role should you consider?
	Contributor
	Owner
	Virtual machine Contributor
	X Storage account Contributor
	Reader

You have an Azure subscription named Subscription1 that contains an Azure Web App named App1. You add the following permissions to the following users:
User1 Owner
User2 Security Admin
User3 Network Contributor
You need to identify which user can assign to another user the Reader role to App1.
	User1, User2, and User3
	User1 and User 2 only
	X User1 only
	User1 and User3 only

You have an Azure subscription named Subscription1. Subscription1 contains a resource group named RG1. RG1 contains resources that were deployed by using templates.
You need to view the date and time when the resources were created in RG1.
Solution: From the RG1 blade, you click Deployments and look for Last modified date.
Does this meet the goal?
	X Yes
	No

You have deployed a VM named “MyVM” in a Resource Group named “myResourceGroup”.
You plan on deleting this VM via PowerShell. The VM is currently in a running state.
Which PowerShell command(s) should you run to perform this action?
	Stop-AzVm -Name MyVM -ResourceGroupName “myResourceGroup”
	Delete-AzVm -Name MyVM -ResourceGroupName “myResourceGroup”
	X Remove-AzVm -Name MyVM -ResourceGroupName “myResourceGroup”


**You have an Azure Subscription in which there is only a Resource Group named “myResourceGroup” created.**
**You are planning on creating a webapp in Azure and deploying code from GitHub on it. You want to do this via Azure CLI.**
**Which command(s) should you run to to successfully configure your solution?**
**Select all options that apply.**
	X az webapp deployment source config --name “myWebapp” --resource-group “MyResourceGroup” --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration.
	? az webapp create –name “myWebapp” --resource-group “myResourceGroup” --plan “myASP”
	? az appservice plan create --name “myASP” --resource-group “myResourceGroup” --location westeurope --sku S1.

You are developing a solution using Azure Service Bus. You need to create a resource group, Service Bus namespace, and a Service Bus queue using Azure CLI. Which three commands should you use?
Select all options that apply.
	az servicebus queue update
	X az group create
	X az servicebus namespace create
	az servicebus namespace update
	X az servicebus queue create

You have an Azure subscription named Subscription1 that contains a ResourceGroup in which multiple resource types have been created (VMs, Webapps, SQL Databases, etc).
You plan on assigning an RBAC role to a user which will need to manage all the operational aspects of these resources but will lack the permission to assign roles to other users. What role should you assign to this user?
	Security Administrator
	Owner
	X Contributor
	Reader

You have deployed multiple VMs in a Resource Group named “myResourceGroup”.
You want to list via PowerShell the location of each VM.
Complete the following script:
$VMs = Get-AzVM -ResourceGroupName MyResourceGroup
Foreach ($vm in $vms) {
[…]
}
	$vm.config.Location
	$vm.HardwareType.Location
	$vm.Location

# C2 Messages and events
You plan on creating an Azure Storage Account that will contain queues. Which type of Storage Account can you consider? Select all options that apply.
	X General-Purpose Storage Accounts v2
	X General-Purpose Storage Accounts v1
	Blob Storage Accounts

-Which authorization methods can you use to successfully make requests to a queue? Select all options that apply.
	 Service Credentials
	X Shared Key
	X Shared Access Signature
	X Azure Active Directory

You are developing an application that needs programmatic access to your queue. Which type from the Azure Storage Client Library for .NET represents a queue instance?
	X CloudQueue
	CloudStorageAccount
	- CloudQueueClient

You are developing an application that needs to programmatically send a message from a queue. Which object should you instantiate to perform this action?
	X CloudQueueMessage
	- CloudQueueClient
	- CloudQueue

Which pieces of information do you need to access a queue? Select all options that apply.
	X Queue Name
	X Storage Account Name
	- Shared Key
	X Authorization Token

True or False? Azure Event Hubs is a cloud-based, event-processing service that can receive and process millions of events per second.
	False
	X True

You plan on using Azure Event Hubs and you want to make sure that the messages will remain available for 5 days even if the data stream needs to be replayed for any reason. Which parameter should you configure?
	- No parameter needs to be set. This will be ensured by default.
	Set the Partition Count parameter to 5.
	X Set the Message Retention parameter to 5.

You plan on configuring an application to send messages to Event Hub. Which information is needed so that the application can create connection credentials?
	X Event Hub Namespace name
	X Primary Shared Access key
	- Storage Account connection string
	X Event Hub name
	X Shared Access Policy name

You plan on using the Azure CLI to retrieve the storage account key from an Azure Storage Account. Which command should you use?
	az storage account show-connection-string
	X az storage account key list
	az list key storage account
	az show-connection-string storage account

You are using Azure Event Hubs and you suspect that the throughput exceeds unit usage. To which metric should you pay attention?
	X Throttled Requests
	Incoming/Outgoing Bytes
	Active Connections

Event Grid is a service that manages the routing and delivery of events from many sources and subscribers.
	False
	X True

Which of the following are some of the main advantages of using Event Grid? Select all options that apply.
	It increases security
	X It supports custom events
	X It can filter events
	X Its throughput is high

You plan on using Event Grid to call a custom endpoint outside Azure. What’s the best way of achieving this?
	Create an Azure Automation event handler that will trigger a script that will call the custom endpoint.
	Create an Azure Functions event handler that will trigger a script that will call the custom endpoint.
	X Create a webhook handler to call the custom endpoint.

You built a mechanism for your environment that will trigger a logic app by using Event Grid. What do you need to do to run actions based on whether the data meets some parameters?
	Build actions
	X Build conditional statements
	Build a recurrence

Which of the following is a view that enables you to edit the JSON configuration of a logic app?
	Designer
	Programmer view
	X Code View

You are developing an e-commerce application. The application generates millions of orders and captures user behavior. Users must be informed as and when there is progress for their order. The application must support the sales and marketing team to analyze live user behavior. Which Azure service should you use to do this?
	Azure Event Grid
	Azure Service Bus
	X Azure Event Hubs

You plan on creating an Azure Event Hub namespace with the help of CLI commands. Which is the command that you should execute?
	az create namespace eventhubs
	X az eventhubs namespace create
	az namespace eventhubs create

You are developing an application that produces millions of telemetry data per hour. You plan to use Azure Event Hubs to ingest and consume data. Which protocols you can use to ingest or consume data? Select all that apply.
	X HTTPS
	X AMQP
	X Kafka

You are developing a solution using Azure Event Hubs. You need to create a resource group, Event Hubs namespace, and an Event Hub using Azure CLI. Which three commands should you use?
	az eventhubs eventhub update
	X az group create
	X az eventhubs eventhub create
	X az eventhubs namespace create

Which terminologies are used to define entities that read data from the Event Hubs? Select all options that apply.
	Publishers
	X Subscribers
	X Consumers

You are planning on using Azure Event Hubs to process events. What is the maximum size limit of a publication of an event?
	256 KB:
	512 KB
	X 1 MB

What are the two programmatic methods that receive and process events from an EventHub? Select two options.
	X EventHubReceiver
	X EventProcessorHost
	EventHostReceiver
	- EventReceiver

Azure Event Grid can distribute events from various Azure resource types. Which of the following can generate events which can be handled by Azure Event Grid?
	- Azure Logic Apps
	X Azure Storage Accounts
	- Azure Virtual Machines
	X Azure Subscriptions
	X Azure Service Bus

Each event that can pass through Event Grid can have a size of up to 128 KB. size limit of an event that can pass through Event Grid?
	X False (each event can be up to 64kb)
	True

A retail chain that has 500 stores is using POS devices to receive payments and collect data. A single device can produce 1.5 megabytes (MB) of data. You need to implement a solution to receive the device data and you also need to correlate the data with the device that it provides it. Solution: Provision an Azure Event Grid. Configure the machine identifier as the partition key and enable capture. Does the solution meet the goal?
	X No
	Yes

A retail chain that has 500 stores is using POS devices to receive payments and collect data. A single device can produce 1.5 megabytes (MB) of data. You need to implement a solution to receive the device data and you also need to correlate the data with the device that it provides it. Solution: Provision an Azure Service Bus. Configure a topic to receive the device data by using a correlation filter. Does the solution meet the goal?
	No
	X Yes

You are developing an e-commerce website that handles millions of orders and captures user behavior. Users must be informed as and when there is progress for their order. Which Azure service should you use to support order processing?
	X Azure Service Bus
	Azure Event Grid
	- Azure Event Hubs
  
You are developing an e-commerce website that handles millions of orders and captures user behavior. Users must be informed as and when there is progress for their order. Which Azure service should you use to respond to events while processing an order?
	? Azure Service Bus
	Azure Event Grid
	- Azure Event Hubs


When using Azure Service Bus programmatically, async methods are also available for interacting with different components. Why are async methods preferred over sync methods?
	X To avoid blocking a thread while waiting on calls to complete
	To improve the security layer of the app
	So that calls will be processed in order, one by one

You are planning on developing a solution that will handle a lot of messages per second through a single queue in Azure Queue Storage. What is the maximum number of messages that can be processed per second, in this case?
	1000 messages per second
	x 2000 messages per second
	5000 messages per second
	10000 messages per second

The Azure Storage client library uses a connection string to establish your connection. Your connection string can only be retrieved via the Azure portal.
	True
	x False

In Event Hubs, partitions are buffers into which communications are saved.
	False
	x True

In Azure Event Grid, system topics are application or third-party topics.
	X False
	True

You are developing a web application for your customer. To ensure a microservices approach, the components of the application are decoupled asynchronous communication. You rely on the order of the messages to map the flow of the data. Which Azure service do you include in your development?
	Azure Notification Hubs
	Event Grid
	- Storage Queues
	- Service Bus

What do you need to access an Azure Storage Queue via REST API?
	X The correct URL that points to the queue and an authorization header included in every request
	The token of the queue
	Only the correct URL that points to the queue, as the authorization is done anonymously

By using Azure Event Hubs in combination with Azure Stream Analytics, you can analyze complex data in near real time.
	Azure Service Bus
	X True

You are developing an application that will interact programmatically with Azure Service Bus. You want to use the library of classes that Microsoft provides and which you can use in any .NET Framework language. What should you do to make use of this library?
	X Install the Microsoft.Azure.ServiceBus NuGet package
	Install a special software that Microsoft provides to use these classes
	Nothing. These classes are automatically included in any development environment

You plan on creating an application for a retail company that will handle different components of a transaction. Services like inventory, payment, and shipping will be managed by different cloud services. What service should you include in your application to ensure asynchronous communication through REST messages about transaction information?
	X Azure Queue Storage
	Azure Blob storage
	Azure Notification Hubs


# C3 Deploy a website using VMs

What is the first thing you should think about when you’re planning to deploy virtual machines in Azure?
	X Network
	OS
	Disk
	Name

What should you create if you want to organize your network (Vnet) into more manageable sections? Select all options that apply.
	X Subnets
	Resource groups
	X Containers

When naming the VM, what are some of the characteristics you should add so you can follow a best practice naming convention? Select all options that apply.
	X Location
	OS
	Disk size
	X Environment
	X Role
	X Instance

What are the aspects that should be considered when choosing the location of your VM? Select all options that apply.
	X Legal or compliance
	X Price
	X Performance
	X Configuration

Which virtual machines size should you chose if you plan to use them for relational databases?
	X Memory optimized
	Compute optimized
	General purpose

Regarding storage for the virtual machine, what is the minimum and maximum number of virtual hard disks (VHDs) that a VM can have?
	2 minimum, maximum 2 per CPU
	1 minimum, maximum 1 per CPU
	- 0 minimum, maximum 5 per CPU

If you want to reduce the maintenance of your virtual machines storage, which type of disks should you set up?
	X Managed
	Unmanaged
	Semi-managed

If you want to automate the deployment of Azure VMs in a programmatic fashion, what tools should you use? Select all options that apply.
	X Azure REST API
	- Azure PowerShell
	- Terraform
	X Azure Client SDK
	- Azure CLI

What should you configure if you want to secure and control every network request coming in or out of your VMs?
	CDN
	X NSGs
	Load balancer

Which virtual machines size should you choose if you plan to use them for model training and deep learning?
	Storage optimized
	Compute optimized
	X GPU

True or False? You cannot change the size of your VM once it has been deployed. You’ll have to delete the VM and create a new one with your desired size.
	True
	X False

You are planning on running a network appliance on a virtual machine. Which workload option should you implement?
	X Compute optimized
	General purpose
	Memory optimized
	Storage optimized

Azure offers different VM sizes that support exclusively Linux based OS images.
	True
	X False

Which VM size category is optimized for production application servers?
	Ls
	X Fsv2, Fs, F
	- Dsv3, Dv3, DSv2, Dv2

What will be the default label for the temporary disk on your Linux VM?
	X /dev/sdb
	/dev/ssd
	/dev/sda

The temporary disk on you VM should not be used to store critical data.
	X True
	False

Besides primary disks and temporary disks, you can add dedicated data disks to your Azure VMs. What is the maximum size of a dedicated disk?
	2,048 GB
	6,096 GB
	15,210 GB
	X 35,183 GB

What is the maximum capacity of the default OS disk for your Linux VM?
	512 GB
	X 2048 GB
	1024 GB

Azure virtual disk sizes are measured in Gibibytes (GiB), which are not the same as Gigabytes (GB). What is the size of 1 GiB compared with 1 GB?
	1 GiB = 1.407 GB
	1 GiB = 1.704 GB
	X 1 GiB = 1.074 GB

True or False? You can create a VHD image from a real disk for your Azure Virtual Machine.
	X True
	False

When using unmanaged disks, how many standard virtual hard disks at full throttle can be supported by a single storage account?
	X 40
	50
	60

Which is the more secure way to connect to your Linux virtual machine using SSH?Connection string
	Username and password
	X SSH keys
	Correct

On Windows 10, Linux, and macOS, what is the built-in command that can generate the SSH public and private key files?
	ssh-genkey
	genkey-ssh
	X ssh-keygen

What port needs be opened on your Azure Linux VM to allow connection via SSH?
	X 22
	44
	86
	3389

For security concerns, you must use an image from the official Azure Marketplace when creating a new virtual machine.
	X True
	False

What are the default quota limits on each subscription regarding VM creation limit?
	40 virtual cores per VM within a region
	20 virtual cores per VM within a region
	X 20 virtual cores across all VMs within a region
	40 virtual cores across all VMs within a region

Which VM size category is optimized for a video editing scenario?
	H
	X NV, NC, NCv2, NCv3, ND
	Esv3, Ev3

On your Azure Windows VM, what is the maximum capacity of your C: drive?
	X 2048 GB
	1024 GB
	4096 GB

Regarding unmanaged disks storage accounts, what is the fixed rate limit of I/O operations/sec?
	12000 I/O operations/sec
	X 20000 I/O operations/sec
	35000 I/O operations/sec

You are configuring a VNET that is making use of the 172.16.0.0/16 address space. You plan on creating a subnet in which you will place a Windows VM. You want this subnet to have 256 IP addresses. What format should the range be?
	X 172.16.1.0/24
	172.16.1.0/25
	172.16.1.0/26

What are the limitations of Azure Windows VM names?
	X between 1-15 characters, cannot contain special or non-ASCII characters, must be unique in resource group
	between 10-15 characters, can contain special characters, must be unique in resource group
	between 10-20 characters, can contain special characters and cannot contain non-ASCII characters

When creating a username and password to connect to your Windows VM, what constraints apply to the format of the password?
	minimum 8 characters long, must have two of the following: one lower case, one upper case, one number and one special character that is not \ or –
	minimum 10 characters long, must have two of the following: one lower case, one upper case, one number and one special character that is not \ or /
	X minimum 12 characters long, must have three of the following: one lower case, one upper case, one number and one special character that is not \ or –

What port number should be opened to be able to connect to your Windows VM using RDP?
	X 3389
	22
	433
You cannot store data on you C: drive along with the OS of you Azure Windows VM.
	True
	X False

What are some methods that enable us to install custom software onto an Azure Windows VM?
	X Custom scripts
	X Custom VM images
	X Remote Desktop Protocol (RDP)

What do you need to configure on your Windows VM if you want to connect to it using RDP via the internet?
	VPN (virtual private network)
	ExpressRoute
	X Public IP

NSG (network security groups) are mandatory at subnet level and optional at network interface level.
	True
	X False

What are the components of the MEAN stack? Select all options that apply.
	X Node.js
	Nugget
	ElasticSearch
	X MongoDB
	Apache
	X AngularJS
	X Express.js
	MySQL

What type of database is MongoDB? Select all options that apply
	Relational
	X NoSQL
	Semi-relational

What are the primary reasons that you should consider when using the MEAN stack? Select all options that apply.
	X Unstructured data
	X JavaScript skilled
	PHP skilled
	Structured data

If you want to create a resource group using the Azure CLI, what command should do the trick?
	X az group create \
	--name <resource-group-name> \
	--location <resource-group-location>
	az resgroup create \
	--name <resource-group-name> \
	--location <resource-group-location>
	az create group \
	--name <resource-group-name> \
	--location <resource-group-location>

If you want to create an Ubuntu VM using the Cloud Shell, what is the correct command?
	X az vm create \
	--resource-group [sandbox resource group name] \
	--name MeanStack \
	--image Canonical:UbuntuServer:16.04-LTS:latest \
	--admin-username azureuser \
	--generate-ssh-keys
	az vm create \
	--resource-group [sandbox resource group name] \
	--name MeanStack \
	--image Canonical:UbuntuServer:16.04-LTS:latest \
	--admin-username azureuser \
	az create vm \
	--resource-group [sandbox resource group name] \
	--name MeanStack \
	--image Canonical:UbuntuServer:16.04-LTS:latest \
	--admin-username azureuser \
	--generate-ssh-keys

Which port do we need to open on the VM to allow HTTP traffic to the web app?
	3389
	443
	22
	X 80

What command should you type in the Azure CLI to open port 80 on your Ubuntu VM?
	az vm open-port-http \
	--port 80 \
	--resource-group [sandbox resource group name] \
	--name MeanStack
	X az vm open-port \
	--port 80 \
	--resource-group [sandbox resource group name] \
	--name MeanStack
	az vm open-port \
	--port 80 \
	--name MeanStack

What are the available MongoDB editions? Select all options that apply.
	MongoDB Standard Server
	MongoDB Premium Edition
	X MongoDB Enterprise Server
	X MongoDB Community Server

You are installing MongoDB from the SSH connection to your Ubuntu VM.
What command should you run in Bash to make sure you have the latest packages?
	sudo apt && sudo apt upgrade
	X sudo apt update && sudo apt upgrade -y
	sudo apt sudo apt upgrade -y

You are installing MongoDB from the SSH connection to your Ubuntu VM. After you installed MongoDB, what command should you run the in Bash to make sure your service started?
	systemctl status mongodb
	sudo status mongodb
	X sudo systemctl status mongodb

You are installing Node.js from the SSH connection to your Ubuntu VM. What command should you run in Bash to register the Node.js repository?
	curl https://deb.nodesource.com/setup_8.x | sudo -E bash –
	curl -sL https://deb.nodesource.com/setup_8.x |
	X curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash –

Why should you make use of AngularJS in the MEAN stack?
	It helps run the web application from the server side.
	It's a browser plugin that gets installed on your user's computer.
	X AngularJS implements data binding for HTML and JavaScript.

You are creating a virtual machine in an Azure subscription named Subscription1 using Azure CLI. Which of the following is a valid value for the --admin-password parameter?
	P@$$w0rd
	abc@123
	P@ssword123
	XPreparationLabs@789

You have an Azure subscription named Subscription1 that contains the virtual machines shown below.
Name Resource Group
VM1 RG1
VM2 RG2
VM3 RG1
VM4 RG2
You need to ensure that the virtual machines in RG1 have the Remote Desktop port closed until an authorized user requests access. What should you configure?
	X just in time (JIT) VM access
	- an application security group
	- a network security group

You are preparing to deploy an Azure virtual machine (VM) based application. The VMs that run the application have the following requirements:
Supporting services must be installed by using an Azure PowerShell script that is stored in Azure Storage.
You need to ensure that the requirements are met.
Which feature should you use?
	X Custom script extension
	Serial console
	Run command
	- Hybrid runbook worker

What is the behavior of the default network security settings for a new virtual machine?
	Neither outbound nor inbound requests are allowed.
	There are no restrictions: all outbound and inbound requests are allowed.
	X Outbound request are allowed. Inbound traffic is only allowed from within the virtual network.

You plan on developing a solution in Azure that will host deep learning models and Machine Learning model training. You chose to build the solution on an IaaS environment, on Virtual Machines. Which size should you choose?
	Storage optimized
	Compute optimized
	X GPU

You plan on developing a solution in Azure that will host an e-commerce application. You chose to build the solution on an IaaS environment, hosting the web servers on Linux Virtual Machines. In order to connect to the VMs to install all the necessary frameworks, what port needs to be opened on your Azure Linux VMs to allow connection via SSH?
	3389
	86
	X 22
	44

You built VMs in your Azure environment and you plan on connecting to them via a private connection from your on-premises servers. What do you need to configure if you want to connect to the Azure VMs using RDP via the private IPs?
	NSGs
	X VPN (virtual private network)
	Public IP

You plan on developing a solution in Azure that will host an e-commerce application. You chose to build the solution on an IaaS environment, hosting the web servers on Windows Virtual Machines. Since the application is intended for commercial use in a secure manner, it needs to allow HTTP and HTTPS traffic. Which port(s) should you open for this? Select all options that apply.
	X 443
	22
	X 80
	3389

You are configuring a MEAN stack in your Azure Environment, and you install MongoDB from the SSH connection to your Ubuntu VM. What command should you run in Bash to make sure you have the latest packages?
	sudo apt sudo apt upgrade -y
	sudo apt && sudo apt upgrade
	X sudo apt update && sudo apt upgrade -y

You are configuring an Azure environment with multiple Virtual Machines. You want to minimize the maintenance as much as possible. Having that in mind, which type of disks should you set up for your VMs?
	Unmanaged
	Semi-managed
	X Managed

You plan on developing a solution in Azure that will host an e-commerce application. You chose to build the solution on an IaaS environment, hosting the web servers on Virtual Machines. Which size should you choose?
	X Compute optimized
	GPU
	Storage optimized

You have an Azure subscription named Subscription1 that contains a virtual machine (VM) named VM1.
You enable just in time (JIT) VM access to VM1.
You need to connect to VM1 by using Remote Desktop.
What should you do first?
	From Azure Active Directory (Azure AD) Privileged Identity Management (PIM), activate the Owner role for the virtual machine.
	From the Azure portal, select the virtual machine VM1, select Connect, and then select Request access.
	From Azure Directory (Azure AD) Privileged Identity Management (PIM), activate the Security administrator user role.
	From the Azure portal, select the virtual machine VM1 and add the Network Watcher Agent virtual machine extension

You built VMs in your Azure environment and you plan on connecting to them via internet. What do you need to configure on your VMs if you want to connect to them?
	X Public IP
	ExpressRoute
	VPN (virtual private network)

You are configuring a MEAN stack in your Azure Environment, and you install MongoDB from the SSH connection to your Ubuntu VM.
After you installed MongoDB, what command should you run the in Bash to make sure your service started?
	systemctl status mongodb
	sudo status mongodb
	X sudo systemctl status mongodb

You are configuring an Azure environment with multiple Virtual Machines. You want to minimize the maintenance as much as possible. Having that in mind, which type of disks should you set up for your VMs?
	Unmanaged
	Semi-managed
	X Managed

# C4 Deploy a website
  
Which are the most popular IDEs for Java development?. Select all options that apply.
	Visual Studio Code
	X Eclipse
	X IntelliJ
	Visual Studio

The Eclipse IDE is used exclusively to build Java applications.
	True
	X False

While the IntelliJ IDEA is widely used for Java development, it also supports an array of different languages via extensible plugins. Which are some of those languages?
Select all options that apply.
	C++
	X JavaScript
	X Scala
	X Ruby

Which of the below is a free source code editor that doesn’t include a compiler?
	IntelliJ
	Eclipse
	Visual Studio
	X Visual Studio Code

Which of the below IDEs provides a full set of tools and features that are specifically targeted at developing apps with Azure? Select all options that apply.
	X Visual Studio Code
	IntelliJ
	Eclipse
	X Visual Studio

When you’re planning to host a web app in Azure, which is the first resource you should deploy inside your Azure subscription?
	A virtual machine
	- A resource group
	X An app service web app
	A virtual network

The Azure App Service belongs to which cloud service model?
	SaaS
	X PaaS
	IaaS

What are deployments slots used for in Azure web apps? Select all options that apply.
	To reserve virtual machine so you can host your web app
	X To test your web app code on Azure
	X To swap your web app between Production and Staging environments
	- To group your web app resources 
		-(No, this is what a resource group does)

Which are the continuous integration/deployment (CI/CD) tools that the Azure Portal provides out-of-box support for your web app? Select all options that apply.
	X GitHub
	X BitBucket
	X local Git repo
	X FTP
	X Azure DevOps

True or False? Azure Web App Service has the built-in ability to automatically scale up/down or scale out. Scaling out is the process of increasing the resources of the underlying machine used to host your web app.
	True
	X False

The company that you work for plans to develop an e-commerce website and deploy it in an Azure web app. You choose to perform a manual deployment of the application and you want to push your code in Azure via Azure CLI. Which feature/command should you use to perform that action?
	az webapp push
	az webapp deployment
	X az webapp up

What are App Service Plans used for in Azure Web apps? Select all options that apply.
	X To determine the billing process for your web app.
	X To determine the App Service features of the web app.
	To determine the strategy of recovering and backing-up your web app.
	X To determine the performance of the machines hosting your web app.

True or False? The number of web apps deployed on a single App Service Plan does not affect the costs of your bill.
	X True
	False

If you want your Azure web app to benefit from features such as Custom Domains/SSL, auto-scale up to 20 instances, at least 3.5 GB RAM, and daily back-ups, which App Service Plan should you chose?
	Dev/test B1
	Prod P2V2
	X Prod P1V2
	Dev/test F1

If you want to build a web app and your preferred development language is C#, which runtime stack should you use on your Azure Web App Service?
	Ruby
	X .NET Core 3.1
	Node 12 LTS
	PHP

If you want to build a web app using Python, which web application framework should you install?
	Node Package Manager (npm)
	Maven
	X Flask
	ASP.NET

Which of the following sources can be configured for automated deployment in Azure? Select all options that apply.
	X OneDrive
	X GitHub
	Mercurial
	X Azure DevOps

True or False? Visual Studio 2019 comes with pre-installed workloads for Azure development and ASP.NET web development.
	True
	X False

How do you install additional workloads in Visual Studio? Select all options that apply.
	X From the Visual Studio console, go to File dropdown then Account settings
	- From the Visual Studio Installer, click Modify
	- From the Visual Studio console, go to File dropdown then Add
	X From the Visual Studio console, go to Tools dropdown then Get tools and features

After installing the ASP.NET Core workload on Visual Studio, alongside ASP.NET, which development languages will also be available for building your web app? Select all options that apply.
	X HTML
	X JavaScript
	Java
	Python

When attempting to create a new simple ASP.NET Core web app project in Visual Studio 2019 on your local machine, what else do you need to configure to kickstart your project?
	X ASP.NET Core Web App
	ASP.NET Core Web App (Model-View-Controller)
	ASP.NET Core Empty
	- ASP.NET Web Application (.NET Framework)

In Visual Studio 2019, which key combination can you press to build the app and run in debug mode?
	Ctrl+F2
	X F5
	Ctrl+F5
	Alt+F4

When Visual Studio creates a web project, which is the port used for the web server?
	44381
	4381
	X Random port
	44352

Which are some of the development languages supported by Azure App Service? Select all options that apply.
	X Java
	X Ruby
	X PHP
	X Python
	- Scala

True or False? There is no limit to the number of web apps you can add to one App Service Plan.
	X True
	False

Which App Service Plan provides the maximum scale-out capabilities and the highest levels of security and performance?
	Standard
	- Premium V2
	Isolated
	Premium

What information do you need to provide so you can publish your local web app to your Azure App Service? Select all options that apply.
	X Subscription
	X Resource group
	X Hosting Plan
	Region
	X Name

After publishing your web app, Visual Studio will structure the project for you. In which folder are the static assets for your site located?
	- Dependencies
	wwwroot
	Properties
	Pages

Which language is used by Razor to create dynamic web pages?
	Java
	X C#
	Python
	Ruby

You have deployed a web application in Azure, and you are using deployment slots to test different versions of the application. Which deployment slot will hold the live web app?
	Staging slot
	X Production slot
	Test slot

How long does it take to swap an instance of a web app from staging to production or the other way around?
	Around 10 minutes
	Less than 30 minutes
	X Instantaneous
	Around 5 minutes

Which App Service Plans allow you to have deployment slots for your web apps? Select all options that apply.
	Basic
	Free
	Shared
	X Premium
	X Isolated
	X Standard

Many of the technologies that developers use to create web apps require final compilation and other actions on the server before they deliver a page to a user. What is this initial delay called?
	X Cold start
	Cold tier
	Cold swap
	Kickstart

True or False? When creating a new deployment slot, if you chose to clone the settings from another slot, this will copy all the content and settings of that slot.
	True
	X False

This scaling process grants more resources to one instance of a web app, the underlying VM onto which the web app is hosted, to handle increased traffic. Which type of scaling is this?
	X Scaling up
	Scaling down
	Scaling in
	Scaling out
	
If you want to increase the availability of your web app, which type of scaling should you approach?
	Scaling up
	Scaling in
	Scaling down
	X Scaling out

If you host your web app on a Basic tier App Service Plan, how many instances can you scale out?
	5
	X 3
	10
	15

If you host your web app on a Premium tier App Service Plan, wow many instances can you scale out?
	X 20 (Creo que está mal. Debería ser 30)
	5
	100
	10

Which App Service plan tiers do not provide availability SLAs? Select all options that apply.
	X Shared
	Standard
	Basic
	Isolated
	Premium
	X Free

A new deployment slot for a web app is just another separate web app with a different hostname and it can be accessed by anyone on the internet if they know that hostname. How can you restrict external access to a deployment slot?
	By applying subscription level policies.
	X By restricting IP addresses.
	By applying RBAC.
	By applying resource locks.

When setting up the git client in Cloud Shell to use it to clone a sample web app, if you want to create a folder for the source code and go inside the folder, which Bash commands should you use?
	az new dir “yourappname”
	az locate “yourappname”
	
	az create folder “yourappname”
	az open “yourappname”
	
	X mkdir “yourappname”
	cd “yourappname”
	
	new dir “yourappname”
	open dir “yourappname”

If you want to commit a new version of a demo web app to git and deploy it to a staging slot using the Cloud Shell on Bash, which command will do the job?
	
	X cd /demoapp/app-service-web-dotnet-get-started
	git add .
	git commit -m "New version of web app."
	git push staging
	
	cd /demoapp/app-service-web-dotnet-get-started
	git commit -m "New version of web app."
	git push staging
	
	/demoapp/app-service-web-dotnet-get-started
	git add .
	git commit -m "New version of web app."
	git push staging
	
	cd /demoapp/app-service-web-dotnet-get-started
	git add .
	git commit -m "New version of web app."
	git push production

If you assign a web app to an existing App Service Plan that contains another web app, how will they behave when you need to scale out one of the web apps? 
	You can configure scale out settings for each of the web apps.
	Only the desired web app will scale out.
	X The web apps will scale out together

When you scale out your web app, how will you be charged?
	Each instance, by resources used.
	- Each instance, by resources available.
	X Each instance, by the hour.

If you need to add features to your web app that will require more computing power, what should you do to meet that demand?
	Remove other web apps from the same plan so you have more resources available
	Scale out
	Move the web app to a higher tier App Service Plan
	X Scale up

What are some possible issues to consider when you scale up a web app? Select all options that apply.
	X New connections to the app might be rejected
	X Web app IP addresses might change
	X Interruptions in service to other client apps
	- Data loss

You plan on creating a Container Registry in a pre-existing resource group named “mygroup” using the CLI. What command should you run?
	X az acr create -name myregistry –resource-group mygroup –sku Standard –admin-enabled true.
	az acr build --file Dockerfile --registry myregistry --image myimage.
	az acr build -name myregistry –resource-group mygroup –sku Standard –admin-enabled true.

True or False? Azure Container Registry enables you to store Docker and Kubernetes images in the cloud, in an Azure storage account.
	True
	X False

You plan on building a Docker image and uploading it to Azure Container Registry. You’ve successfully cloned a Git repository which contains all the necessary files to build your docker image. What CLI command should you use?
	az acr create --file Dockerfile --registry myregistry --image myimage.
	- az acr build -name myregistry –resource-group mygroup –image myimage.
	X az acr build --file Dockerfile --registry myregistry --image myimage.

When a webapp is created from a docker image, which property represents the name of the repository?
	Tag
	- Registry
	X Image

You plan on creating a Container Registry task from the command line. Which command should you run?
	az acr register task
	X az acr task
	az acr build task

What kind of service is Azure App Service using to support continuous deployment?
	Logic apps
	Functions
	X Webhooks
	Workloads

You have a docker image of a web app hosted in Azure Container Registry. You want to monitor the GitHub repository of the image and take action automatically whenever the source code changes. What feature of the ACR can help you achieve that?
	Jobs
	X Tasks
	- Monitoring
	- Updates

True or False? Azure Container Registry tasks can only be created from the command line.
	X True
	False

Before creating a ACR task, what should be configured on GitHub in order to have the necessary permissions to create a webhook in the repository?
	X Personal access token (PAT)
	Private access token (PAT)
	Shared access token (SAS)
	Admin username and password

Which command should you run in the CLI to set up an Azure Container Registry task?
	az acr new task
	X az acr task create
	az new acr task
	az create new acr task

If you want to get a list of all the container registries in your subscription in the form of a table, which CLI command should you run?
	az acr list
	X az acr list -o table
	az acr get list – o table
	a acr get list

If you want to import a large docker image from an ACR to another ACR without waiting for completion, what command should you run in the CLI?
	az acr import -n MyRegistry --source sourceregistry.azurecr.io/sourcerepository:sourcetag --wait-none
	az acr import -n MyRegistry --source sourceregistry.azurecr.io/sourcerepository:sourcetag --wait-no
	az acr import -n MyRegistry --source sourceregistry.azurecr.io/sourcerepository:sourcetag --wait 0
	X az acr import -n MyRegistry --source sourceregistry.azurecr.io/sourcerepository:sourcetag --no-wait

You are developing an application named Application1. The Application1 consumes a web service hosted in your on-premise network. You are creating an Azure App Service to deploy Application1. Which app service plans should you consider to host Application1? Select all options that apply.
	-Basic
	-Free
	X Premium
	X Standard

Fourth Coffee has an ASP.NET Core web app that runs in Docker. The app is mapped to the www.fourthcoffee.com domain. Fourth Coffee is migrating this application to Azure.
You need to provision an App Service Web App to host this docker image and map the custom domain to the App Service web app.
A resource group named FourthCoffeePublicWebResourceGroup has been created in the WestUS region that contains an App Service Plan named AppServiceLinuxDockerPlan.
In what order should the CLI commands be used to develop the solution?
1. az webapp config container set
--docker-custom-image-name
$dockerHubContainerPath
--name $appName
--resource-group
fourthCoffeePublicWebResourceGroup
2. az webapp config hostname add
--webapp-name $appName
--resource-group
fourthCoffeePublicWebResourceGroup \
--hostname $fqdn
3. az webapp create
--name $appName
--plan AppServiceLinuxDockerPlan
--resource-group
fourthCoffeePublicWebResourceGroup
4. #/bin/bash
appName = “FourthCoffeePublicWeb$random”
location= “WestUS”
dockerHubContainerPath = “FourthCoffee/publicweb.v1”
fqdn = www.fourthcoffee.com
	1, 2, 3, 4.
	- 4, 3, 2, 1.
	4, 3, 1, 2.

You have an Azure Container Registry named Registry1. You need to publish an Image named Image1 to Finance namespace. Which of the below commands should you use?
	docker push registry1.azurecr.io/finance/image1
	- docker push registry1.azurecr/finance/image1
	docker push finance.azurecr/registry1/image1
	docker push finance.azurecr.io/registry1/image1

You have a server named Server1 that runs Windows Server 2019. Server1 is a container host.
You are creating a Dockerfile to build a container image.
You need to add a file named File1.txt from Server1 to a folder named C:\Folder1 in the container image.
Solution: You add the following line to the Dockerfile.
COPY File1.txt /Folder1/
You then build the container image.
Does this meet the goal?
	X Yes
	No

You have an Azure Container Registry named Registry1. You add role assignment for Registry1 as shown in the following table.
User Role
User1 AcrPush
User2 AcrPull
User3 AcrImageSigner
User4 Contributor
Which users can upload images to Registry1?

User4 and User1
User1
- User4, User3, and User1
User4

You have a web app named WebApp1 that uses an Azure App Service plan named Plan1. Plan1 uses the D1 (Shared) pricing tier and has an instance count of 1.
You need to ensure that all connections to WebApp1 use HTTPS.
What should you do first?
	X Scale up Plan1
	Disable anonymous access to WebApp1
	Scale out Plan1
	Modify the scale settings for WebApp1

A company is developing a Java web app. The web app code is hosted in a GitHub repository located at https://github.com/company/webapp.
The web app must be evaluated before it is moved to production. You must deploy the initial code release to a deployment slot named staging.
You need to create the web app and deploy the code.
How should you complete the following commands?
gitrepo=https://github.com/company/webapp
webappname=businesswebapp
resourcegroupname=businessappresourcegroup

az group create --location centralus --name $resourcegroupname
az appserviceplan create --name $webappname --resource-group $resourcegroupname --sku S3
az webapp create --name $webappname --resource-group $resourcegroupname --plan $webappname
az webapp deployment slot create --name $webappname --resource-group $resourcegroupname --slot staging
az webapp deployment source config --name $webappname --resource-group $resourcegroupname \
--slot prod --repo-url $gitrepo --branch master --manual-integration

az group create --location centralus --name $resourcegroupname
az webapp create --name $webappname --resource-group $resourcegroupname --sku S3
az appserviceplan create --name $webappname --resource-group $resourcegroupname --plan $webappname
az webapp deployment slot create --name $webappname --resource-group $resourcegroupname --slot staging
az webapp deployment source config --name $webappname --resource-group $resourcegroupname \
--slot staging --repo-url $gitrepo --branch master --manual-integration

X az group create --location centralus --name $resourcegroupname
az appserviceplan create --name $webappname --resource-group $resourcegroupname --sku S3
az webapp create --name $webappname --resource-group $resourcegroupname --plan $webappname
az webapp deployment slot create --name $webappname --resource-group $resourcegroupname --slot staging
az webapp deployment source config --name $webappname --resource-group $resourcegroupname \
--slot staging --repo-url $gitrepo --branch master --manual-integration

You have deployed a web app to an app service named myappservice. Your security administrator has advised you to prevent all connections from an IP address of 11.0.0.11.
You need to modify myappservice to successfully prevent the connections from the IP address. The design must minimize Azure-related costs. What should you do?
	Configure Azure CDN
	Configure Service Endpoint
	Change App Service plan to Premium
	X Configure IP Restrictions

You are architecting a solution and you realize that you need an Azure Container Registry to host your app images. You plan on automating the deployment through CLI commands. What command should you include in your script to create the Azure Container Registry?
	az acr build -name myregistry –resource-group mygroup –sku Standard –admin-enabled true.
	az acr build --file Dockerfile --registry myregistry --image myimage.
	X az acr create -name myregistry –resource-group mygroup –sku Standard –admin-enabled true.

You are the Azure administrator of the e-commerce company buyeverything.com. The webapp is being hosted in Azure in an S2 plan. You notice that from time to time, the platform drops some of the requests due to a high load of customers. What should you do to ensure availability at any time?
	Manually scale-up when the app has performance issues
	X Implement auto-scale rules to scale-out
	Manually scale-out when the app has performance issues

You plan to create a Docker image that runs an ASP.NET Core application named MyApp. You have a setup script named setupScript.ps1 and a series of application files including MyApp.dll.
You need to create a Dockerfile document that meets the following requirements:
Call setupScripts.ps1 when the container is built.
Run MyApp.dll when the container starts.
The Dockerfile document must be created in the same folder where MyApp.dll and setupScript.ps1 are stored.
Which five commands in sequence should you use to develop the solution?
	WORKDIR /apps/MyApp
	Copy ./ .
	FROM microsoft/aspnetcore:latest
	RUN powershell ./setupScript.ps1
	CMD [“dotnet”, “MyApp.dll”]
	
	X FROM microsoft/aspnetcore:latest
	WORKDIR /apps/MyApp
	Copy ./ .
	RUN powershell ./setupScript.ps1
	CMD [“dotnet”, “MyApp.dll”]
	
	FROM microsoft/aspnetcore:latest
	WORKDIR /apps/MyApp
	Copy ./ .
	CMD [“dotnet”, “MyApp.dll”]
	RUN powershell ./setupScript.ps1

You are planning to deploy an application named Application1 in an Azure App Service. You need to eliminate file conflicts between deployments and improve cold-start performance. Which setting should you configure in your Azure App Service?
	Set WEBSITE_RUN_FROM_PACKAGE=0
	Set WEBSITE_RUN_FROM_PACKAGE=1
	Set Always On to Off
	- Set Always On to On

You are the Azure administrator of the e-commerce company buyeverything.com. The webapp is being hosted in Azure in an S2 plan, configured to auto-scale up-to 5 instances based on CPU percentage. You notice that the app has performance issues – the pages load slowly and some of the components are not loading. What should you do?
	Restart the webapp
	Scale-up the webapp to S3
	- Implement auto-scale rules to scale-out

You are architecting a solution and you realize that you need to build your docker image and upload it to Azure Container Registry. You plan on automating the deployment through CLI commands. Your automation clones a Git repository that contains all the necessary files. What command should you include in your script to build the docker image and upload it to Azure Container Registry?
	X az acr build --file Dockerfile --registry myregistry --image myimage.
	az acr build -name myregistry –resource-group mygroup –image myimage.
	az acr create --file Dockerfile --registry myregistry --image myimage.

You are the Azure administrator of the e-commerce company buyeverything.com. The webapp is being hosted in Azure in an S2 plan, configured to auto-scale up-to 5 instances based on CPU percentage. You notice that the app has performance issues – the pages load slowly and some of the components are not loading. What should you do?
	Implement auto-scale rules to scale-out
	Restart the webapp
	X Scale-up the webapp to S3

#C5 

Many Azure services include built-in security features however Azure also has specific tools to assist with securing your environment. Which of the following would be the simplest way to monitor your resources and perform automatic security assessments to identify potential vulnerabilities?
	X Azure Security Center
	Azure Key Vault
	Azure Sentinel

Your company has migrated to Azure Cloud services. Management wants to implement security that will limit the applications that can run on certain virtual machines. Which of the following approaches provide such a solution?
	Connect the virtual machines to Azure Sentinel.
	X Implement an application control rule in Azure Security Center.
	Administrators periodically review what applications are running on each VMs by creating and running PowerShell scripts.

Your company has recently migrated to Azure cloud services. Azure has various reporting and monitoring tools built in. What is the simplest tool to use to create a single report that will show all security information to be collected from all the monitoring tools?
	Azure Key Vault
	- Secure Score
	X Azure Sentinel

Your company had recently migrated to Azure cloud services and management are concerned that sensitive information such as passwords, encryption keys, and certificates will not be as secure as they were when operating an on-premises environment. What solution can you implement to allay these concerns?
	Configure a secure VM and store the Passwords and certificates in a shared folder.
	Implement Azure Sentinel.
	X Implement Azure Key Vault.

Your company is planning to migrate to Azure cloud services however because of their type of business they are obliged to follow regulatory compliance that requires them to be the only customer using the physical machine that will host their virtual machines in the cloud. How can your company migrate to the cloud while still remaining compliant?
	Configure the network so that the company’s VMs are isolated from other VM’s running on the same host in the datacenters.
	X Configure the VM’s to run on Azure Dedicated Host
	They cannot, these specific systems will need to remain and operate on-premises only.

True or False? Azure Security Center can only monitor Azure cloud services.
	True
	X False

Which two of the following are Azure Security Center offering tiers that you can choose from?
	Premium
	X Free
	Basic
	X Standard

What is the price model of the ASC Standard tier?
	15$/VM per month
	X 15$/node per month
	15$/application per month
	15$/ month

To make sure you sanitize your input data, which three of the data sources below need to be validated?
	X Data from a third-party API.
	Data sent to a third-party API.
	X Data from the user input fields.
	X Data from the URL parameter.

In order to avoid Cross-Site Scripting (XSS) attacks, which of the following data sources need to be encoded?
	Data sent to a third-party API.
	Data saved to a database.
	- Data in the URL parameters.
	X Data to be output on the screen.

Which of the following snippets is an example of a parametrized SQL statement?
	X -- Lookup a user CREATE PROCEDURE sp_findUser ( @UserName varchar(50) ) SELECT * FROM [dbo].[users] WHERE userName = @UserName
	
	string userName = Request.QueryString["username"]; ... string query = "SELECT * FROM [dbo].[users] WHERE userName = '" + userName + "'";
	
	string userName = Request.QueryString["username"]; // receive input from the user ... string query = "SELECT * FROM [dbo].[users] WHERE userName = '" + userName + "'";

True or False? Azure Key Vault’s purpose is to store configuration secrets for the server-side of the app, not the client-side of the app.
	X True
	False

Which of the following canbe stored in an Azure Key Vault? Select all that apply.
	Logs
	X File locks
	X Secrets
	X Access policies
	X Passwords
	X Connection strings
	X Certificates
	X Automation scripts

What are the three states of digital data?
	X Data at rest
	X Data in transit
	Cold tier data
	Hot tier data
	X Data in process

Which one of the following solutions can be used to protect data at rest, and resides on the Infrastructure-as-a-Service cloud model?
	Azure VPN Gateway
	Azure SQL Database
	Azure Storage
	X Azure Disk Encryption

Which of the following solutions can be used to protect data in transit? Select all that apply.
	X HTTPS protocol
	X SSL/TLS protocols
	Azure Storage
	X Azure VPN Gateway
You want to secure access from multiple workstations located on-premises to an Azure virtual network. What feature should you implement in order to encrypt data in transit?
	X Site-to-site VPN
	Azure ExpressRoute
	- Point-to-site VPN

In the SQL Information Protection Paradigm, which feature allows you to scan your database to identify columns with potentially sensitive data?
	Query result set sensitivity
	Visibility
	Labeling
	X Discovery and recommendations

Azure Storage supports Azure Active Directory and role-based access control (or RBAC) for both resource management and data operations. You can assign RBAC roles that are scoped to which of the following? Select all options that apply.
	X An individual container or queue
	X A Resource group
	Table
	X A storage account
	X A subscription,

Azure Storage accounts can create authorized apps in Active Directory to control access to the data in which of the following? Select all options that apply.
	X Azure Blobs
	Azure Tables
	X Azure Queues
	Azure Files

In Azure Storage, clients can use a shared key or shared secret for authentication and to restrict access to resources. A Shared key is supported by which of the following storage models? Select all options that apply.
	X Tables
	X Queues
	Disks
	X Files
	X Blobs

True or False? In Azure Storage accounts, shared keys give access to everything in the account.
	X True
	False

You are required to grant access to a third-party app that uploads pictures to one of your Blob Stores. From a security perspective which of the following is recommended to delegate access and specify constraints such as permissions?
	Storage Account Key
	X Shared Access Signature (SAS)
	Azure Active Directory

You have an Azure Storage service that must handle large amounts of data and high-volume transactions. Which of the following solutions in your opinion would be the most appropriate to reduce complexity and cost while still providing authentication?
	Front end proxy server
	X lightweight Service

Which of the SQL Information Protection (SQP IP) services and capabilities allows you to limit data exposure to non-privileged users?
	X Dynamic data masking
	Azure SQL Auditing
	- Security Center
	Transparent data encryption
	- Data Discovery & Classifications

Which one of the following SQL Information Protection (SQP IP) services and capabilities allows you to encrypt data at rest without any changes to your application?
	Azure SQL Auditing
	- Security Center
	X Transparent data encryption
	Data Discovery & Classifications

Is the write once, read many (WORM) states’ only ability to make the data unerasable?
	X No
	Yes

In terms of immutable storage and data retention, which one of the following data retention policies should be implemented when the retention interval is not agreed upon?
	Basic retention policy
	X Legal hold retention policy
	Undetermined retention policy
	Time-based retention policy

Identify three primary concepts used in Azure Key Vault.
	X Vaults
	X Secrets
	Treasury
	X Keys

Which two PowerShell and Azure CLI commands can you use to create a new vault in a resource group?
	az create keyvault \ --resource-group <resource-group> \ --name <your-unique-vault-name>

	X New-AzKeyVault -Name <your-unique-vault-name> -ResourceGroupName <resource-group>

	- AzKeyVault-new -Name <your-unique-vault-name> -ResourceGroupName <resource-group>

	X az keyvault create \ --resource-group <resource-group> \ --name <your-unique-vault-name>


True or False? Key vaults enable you to control and log access to anything stored in them.
	False
	X True

Which type of asymmetric keys are used in Azure Key Vault service?
	RSA 1024
	RSA 280
	RSA 1536
	X RSA 2048

What is the average size of a secret in an Azure Key Vault?
	500KB
	1MB
	100KB
	X 10KB

What is the maximum number of Azure Active Directories that can be associated with one Azure subscription?
	X1
	10
	3

True or False? Roles assigned at a parent scope, such as a resource group, are not inherited by the child scope, such as resources in that resource group.
	XFalse
	True

Which three of the following scenarios can you implement with Azure RBAC?
	Allow users to sign in using multi-factor authentication.
	X Allow one user to manage virtual machines in a subscription and another user to manage virtual networks.
	X Allow an application to access all resources in a resource group.
	X Allow a database administrator group to manage SQL databases in a subscription.
	Allow a webapp to be accessed only from a desired range of IP.

Azure RBAC works by making use of three elements known as the who, what, and where. Which one of the following is the "who" element?
	Role definition
	Scope
	XSecurity principal

Which of the following built-in roles allows a user to manage a resource and grant access to that resource?
	Reader
	Contributor
	X Owner
	User Access Administrator

True or False? Azure Key Vault does not support anonymous access.
	X True
	False

User1 must be able to create Azure Key Vaults, but should not be able to access the data or grant access to the data contained by the Key Vault. What role should fit the requirements of User1?
	X Key Vault Contributor
	User Access Administrator
	Owner
	Key Vault Administrator

You are configuring a Key Vault access policy. User2 is a developer and must have read-only permission. Which two of the following Key permissions should you assign to User2?
	Update
	X Get
	Create
	X List

You are planning to add a certificate to an Azure Key Vault. The lifecycle of the certificate must be managed and monitored from the Key Vault. How should you add the certificate?
	Create self-signed certificates from the Azure portal.
	Import existing certificates
	- Create an X.509 certificate signing request (CSR).
	X Connect your Key Vault with a trusted certificate issuer (integrated CA) and create the certificate directly in Azure Key Vault.

You are unable to view resources deployed in a specific resource group. How should the administrator verify your access?
	Go to one of the resources in the resource group and select Role assignments.
	X Go to the resource group and select Access control (IAM) > Role assignments.
	Verify your permissions by going to the Azure profile > My permissions.

You are the administrator in your team. Your project manager has asked you to generate a report of the role assignments for the last month. How would you generate this report using the Azure portal?
	X Search for Activity log and filter on the Create role assignment (roleAssignments) operation.
	At the applicable scope, go to Access control (IAM) > Role assignments.
	At the applicable scope, go to Access control (IAM) > Download role assignments.

One of the administrators in another team has requested access to a virtual machine managed by your team. Following the least-privilege best practice, how should you resolve this request?
	X At the resource scope, assign the role with the appropriate access.
	At the resource group scope, assign the role with the appropriate access.
	At the resource scope, create a role for them with the appropriate access

You need to create an Azure SQL Database logical server using the Azure CLI. Which command should you choose?

	create az sql server \ --name $SERVERNAME \ --resource-group $RESOURCEGROUP \ --location $LOCATION \ --admin-user $ADMINLOGIN \ --admin-password $PASSWORD
	
	X az sql server create \ --name $SERVERNAME \ --resource-group $RESOURCEGROUP \ --location $LOCATION \ --admin-user $ADMINLOGIN \ --admin-password $PASSWORD
	
	az create sql server \ --name $SERVERNAME \ --resource-group $RESOURCEGROUP \ --location $LOCATION \ --admin-user $ADMINLOGIN \ --admin-password $PASSWORD
	
	az sql create server \ --name $SERVERNAME \ --resource-group $RESOURCEGROUP \ --location $LOCATION \ --admin-user $ADMINLOGIN \ --admin-password $PASSWORD

You now need to create a database namedmarketDB on top of the SQL server you created earlier. You can use the WorksLT database as a template so as to have some pre-populated tables to work with. What is the correct Azure CLI command for the job?

	az sql db create --resource-group RESOURCEGROUP \ --server SERVERNAME \ --name marketDB \ --sample-name WorksLT \ --service-objective Basic
	
	az sql create --resource-group $RESOURCEGROUP \ --server $SERVERNAME \ --name marketDB\ --service-objective Basic
	
	X az sql create --resource-group RESOURCEGROUP \ --server SERVERNAME \ --name marketDB \ --sample-name WorksLT \ --service-objective Basic
	
	az sql db create --resource-group $RESOURCEGROUP \ --server $SERVERNAME \ --name marketDB \ --sample-name WorksLT \ --service-objective Basic

Now you’ll want to get the connection string for the database. Which Azure CLI command should do the job?

	X az sql db show-connection-string --client sqlcmd --name marketplaceDb --server $SERVERNAME | jq -r
	
	az sql db append-connection-string --client sqlcmd --name marketDB --server $SERVERNAME | jq -f
	
	az sql db reveal-connection-string --client sqlcmd --name marketDB--server $SERVERNAME | jq
	
	az sql db list-connection-string --client sqlcmd --name marketDB --server $SERVERNAME | jq -s

Which process term refers to what an identity can do within an Azure SQL Database?

	Authentication
	
	X Authorization
	
	Auditing

True or False? You can connect to a Linux VM over SSH without a password if you generated the SSH Keys for that VM.
	
	False
	
	X True

You have an Azure SQL Database on an Azure SQL Database server. You also created a Linux VM. You need to be able to connect to your database from your Linux VM throughsqlcmd.
What should you install on the Linux VM to provide connection?
	
	-Azure Toolkit
	
	npm
	
	Node.js
	
	X mssql-tools


On an Azure SQL Database logic server, which firewall rules can be configured at the database level?

	X IP address rules.
	
	Allow access to Azure services.
	
	Virtual network rules.
	
You have several Azure VMs that need access your Azure SQL Databases. What infrastructure security rules should you implement?

	X Virtual network rules.
	
	Allow access to Azure Services.
	
	IP address rules.

You need to connect to a database from a Linux VM using the connection string of the database. Which sqlcmd command should you use?

	sqlcmd -Q tcp:serverNNNN.database.windows.net,3389 -d marketDB -U '[username]' -P '[password]' -N -l 30
	
	X sqlcmd -S tcp:serverNNNN.database.windows.net,1433 -d marketDB -U '[username]' -P '[password]' -N -l 30
	
	sqlcmd tcp:serverNNNN.database.windows.net,1433 -d marketDB -U '[username]' -P '[password]' -N
	
	sqlcmd -S tcp:serverNNNN.database.windows.net,3389 -d marketDB -U '[username]' -P '[password]' -N


You have a server-levelIP rule to restrict the systems that can connect. You want to delete that rule using the sqlcmd prompt. Which command is suitable for this task?
	
	az sql sp_delete_database_firewall_rule N'My Firewall Rule'; GO
	
	az-rm sql sp_delete_database_firewall_rule N'My Firewall Rule'; GO
	
	RUN sp_delete_database_firewall_rule N'My Firewall Rule'; GO
	
	X EXECUTE sp_delete_database_firewall_rule N'My Firewall Rule'; GO


True or False? Transparent data Encryption (TDE) performs real-time encryption and decryption of the Azure SQLdatabase, associated backups, and transaction log files at rest without requiring changes to the application.

	False
	
	X True


From your Linux VM, you connected to your Azure SQL Database server and created a new user called AppUser1. You now want to grant the data reader and data writer roles to AppUser1. Which one of the following T-SQL commands should you use to grant those roles?
	
	MODIFY ROLE db_datareader ADD MEMBER AppUser1; MODIFY ROLE db_datawriter ADD MEMBER AppUser1; GO
	
	GRANT ROLE db_datareader TO MEMBER AppUser1; GRANT ROLE db_datawriter TO MEMBER AppUser1; GO
	
	- ALTER ROLE db_datareader FOR MEMBER AppUser1; ALTER ROLE db_datawriter FOR MEMBER AppUser1; GO
	
	X ALTER ROLE db_datareader ADD MEMBER AppUser1; ALTER ROLE db_datawriter ADD MEMBER AppUser1; GO

  

You have an application named Application1. Application1 generates log files that must be archived for seven years. The log files must be readable by Application1 but must not be modified.
Which storage solution should you use for archiving?

	X Use an Azure Blob storage account and a time-based retention policy.
	
	Ingest the log files into an Azure Log Analytics workspace.
	
	Use an Azure file share that has access control enabled.
	
	-Use an Azure Blob Storage account configured to use the Archive access tier.


You have an Azure Storage account _namedmystorageaccount_, which contains several files of 1GB named File1, File2, File3 and so on. The files are set to use the archive access tier. You need to ensure that File1 is accessible immediately when a retrieval request is initiated.
Would changing the access tier to Hot meet this goal?
	
	X Yes
	
	No


You have an Azure Storage v2 account named storage1. You plan to archive data to storage1. You need to ensure that the archived data cannot be deleted for five years. The solution must prevent administrators from deleting the data.
Would creating an Azure Blob storage container and configuring a time-based retention policy meet this goal?
	
	X Yes
	
	No


You are developing an application. You have an Azure user account that has access to multiple subscriptions. You need to store and retrieve a storage account key secret from Azure Key Vault.
In which order should you arrange the following PowerShell commands to develop the solution?
1. Get-AzStorageAccountKey -ResourceGroupName $resGroup -Name $storAcct
2. Get-AzKeyVaultSecret -VaultName $vaultName
3. Get-AzSubscription
4. $secretvalue =ConvertTo-SecureString $storAcctKey -AsPlainText -Force Set-AzKeyVaultSecret -VaultName $vaultName -Name $secretName -SecretValue $secretvalue
5. Set-AzContext -SubscriptionId $subscriptionID
	
	3, 2, 1, 4, 5
	
	X3, 5, 1, 4, 2
	
	1, 2, 3, 4, 5


You are designing a solution to secure a company's Azure resources. The environment hosts 10 teams. Each team manages a project and is comprised of a project manager, a virtual machine (VM) operator, developers, and contractors.
Project managers must be able to manage everything except access and authentication for users. VM operators must be able to manage VMs, but not the virtual network or storage account to which they are connected. Developers and contractors must be able to manage storage accounts.
You need to provide access for the Virtual Machine Operator. What role should you provide them with?

	Storage account contributor
	
	Owner
	
	Contributor
	
	X Virtual machine contributor

You are developing a solution to secure a company's Azure resources. The Azure environment is used by 10 teams. Each team manages a project and is comprised of a project manager, a virtual machine (VM) operator, developers, and contractors.
Project managers must be able to manage everything except access and authentication for users. VM operators must be able to manage VMs, but not the virtual network or storage account to which they are connected. Developers and contractors must be able to manage storage accounts.
What role should you recommend for the Project Manager?
	
	X Contributor
	
	Reader
	
	Virtual machine contributor
	
	Owner


You are developing a medical records document management website. The website is used to store scanned copies of patient intake forms. If the stored intake forms are downloaded from storage by a third party, the contents of the forms must not be compromised. You need to store the intake forms according to the requirements.
Would storing the intake forms as Azure Key Vault secrets meet your goal?

	X No
	
	Yes


You download an Azure Resource Manager template based on an existing virtual machine. The template will be used to deploy 100 virtual machines. You need to modify the template to reference an administrative password. You must also prevent the password from being stored in plain text.
Which of the following should you create to store the password?

	X An Azure Key Vault and an access policy.
	
	An Azure Storage account and an access policy.
	
	An Azure Active Directory (AD) Identity Protection and an Azure policy.


You have an Azure SQL Database instance. Database management is performed by an external party. All cryptographic keys are stored in an Azure Key Vault. You must ensure that the external party cannot access the data in the SSN column of the Person Table.
Would storing column encryption keys in the system catalog view in the database suffice as a method of protection?

	X No
	
	Yes
Would enabling the Always encrypted feature qualify as a sufficient method of protection?
	X Yes
	No

You are developing an application using Azure web app and Azure SQL Server. You need to implement dynamic data masking on a column that stores social security numbers as a string in the format "123-45-6789". You want to mask everything except the last four digits.
Which data masking function and replacement string should you choose to fulfill this requirement?

	- Text: XXXX-XX-
	
	- Default: XXXX
	
	Email: aXX@XXXX.com
	
	Credit card: XXXX-XX-

  
You are developing an application to host within Azure Virtual Machines (VMs). The application interfaces with external services which are authenticated using a secret key. You are considering Azure Key Vault to store secret keys.
What authentication method must you consider for reading secrets from Key Vault from Azure Virtual Machines (VMs)?

	X Managed Identity
	
	Service principal and certificate
	
	Service principal and secret

You have an Azure App Services Web App, Azure SQL Database instance, Azure Storage Account, and an Azure Redis Cache instance in a resource group. A developer must be able to publish code to the web app. To facilitate this, you must grant the developer the Contributor role to the web app.
Which two commands can you use to assign this role? Note that each correct answer presents a complete solution.
	
	New-AzureRmRoleDefinition
	
	X New-AzRoleAssignment
	
	az role definition create
	
	X az role assignment create

You are developing a medical records document management website. The website is used to store scanned copies of patient intake forms. If the stored intake forms are downloaded from storage by a third party, the contents of the forms must not be compromised. You need to store the intake forms according to the requirements.
Would the following solution meet your goal?:
1. Create an Azure Key Vault key named "skey".
2. Encrypt the intake forms using the public key portion of skey.
3. Store the encrypted data in Azure Blob storage.

	No
	
	X Yes

You have an Azure subscription named Subscription1 that contains a virtual machine (VM) named VM1. You enable just in time (JIT) VM access to VM1. You need to connect to VM1 by using Remote Desktop.
What action should you perform first to enable this connection?

	From Azure Active Directory (Azure AD) Privileged Identity Management (PIM), activate the Owner role for the virtual machine.
	
	From the Azure portal, select the virtual machine VM1 and add the Network Watcher Agent virtual machine extension.
	
	X From the Azure portal, select the virtual machine VM1, select Connect, and then select Request access.
	
	From Azure Directory (Azure AD) Privileged Identity Management (PIM), activate the Security administrator user role.


You have an Azure Storage v2 account named storage1. You plan to archive data to storage1. You need to ensure that the archived data cannot be deleted for five years. The solution must prevent administrators from deleting the data.
Would creating an Azure Blob storage container and configuring a legal hold access policy meet this goal?

	Yes
	
	X No