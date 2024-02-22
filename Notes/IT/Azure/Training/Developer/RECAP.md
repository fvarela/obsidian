You want to develop an application that can be executed with a couple of modules.
Which Azure services should you use in order to have a minimal operating costs value and minimal admin activities?
	Azure Web App
	Azure Functions
	- Azure Logic Apps
	Azure Virtual Machine

Azure Function in App Service plan. Enable 'Always ON' feature.

Azure App Service vs Durable Functions.
Azure App Service is just for web apps!

You are using an Azure API Management managed web service. HTTP Strict Transport Security (HSTS) is implemented in the back-end web service. For every request made to the back-end service you must have a valid HTTP authorization header. Also, your Azure API Management instance must include an authentication policy.
Which of the below policies are fit for use?
	X Certificate Authentication
	Digest Authentication
	Basic Authentication
	- OAuth Client Credential Grant


You want to capture user behaviour and handle millions of orders through the e-commerce website that you are developing. You want to inform users if and when progress is made for the order they placed.
If you need to respond to events during the order processing, which Azure service would be the most appropriate?
	Azure Event Hubs
	- Azure Service Bus
	Azure Event Grid



You plan to develop a web application for your customer. The components of the application are not coupled, having an async/microservices approach. For mapping the flow of the data, you rely on the order of the messages.
Considering this scenario, what Azure service do you need to include in the development?
	Azure Notification Hubs
	Event Grid
	Storage Queues
	X Service Bus



Type of Blobs:
	Page Blobs (For random access such a VM HD)
	Block Blobs (Text, binary, vídeos...)
	Append Blobs (Append operations such as logging.)


Create a container if it does not exist with c#:
	container.CreateIfNotExists()

Ports:
	SSH 22
	RDP 3389

Webapps and webapps slots.

How to assign roles both in azure powershell and cli






rehydration priority options 
	High (Before standard. It might take less than an hour)
	Standard (It goes to a queue. Takes up to 15 hours.)
What Storage solution is the most suitable to save an VM image
	Blob Storage
Create containers using the .net library. What function to call. ->
	container.CreateIfNotExists();
Available APIs for accessing Cosmos DB
	NoSQL, MongoDB, PostgreSQL, Cassandra, Gremlin, Table
Check location of Virtual machines using powershell
	
CLI command to delete a running VM
	az vm delete --resource-group myResourceGroup --name myVM --yess
What is Azure CDN?
	Azure Content Delivery Network. It stores cached content on the edge servers.

Durable functions. Patterns:
	Function chaining
	Fan-out/fan-in
	Async HTTP APIs
	Monitoring
	Human interaction
	Aggregator (stateful entities)

Durable functions. Types:
	Orchestrator. Describe how actions are executed. Javascript or C#
	Activity. The basic units of work.
	Entity. Handle state
	Client. Any function can be a client function.

Available plans in Azure Functions Hosting:
	Consumption plan. Scale automatically. Cold start
	Premium plan. Scale automatically. Prewarmed. More CPU or memory. Your code needs to run longer.
	Dedicated plan. You have existing underutilized VMS

  
You are using PowerShell for creating a virtual machine in your Azure subscription. Considering this, what should be the next two parameters that you should use in order to complete the following command?

New-AzVm -Name "myVM" -Location "East US" -SubnetName "mySubnet" -SecurityGroupName "myNetworkSecurityGroup" -PublicIpAddressName "myPublicIpAddress" -OpenPorts 80,3389
	- -DiskSize 4096
	-ResourceGroupName "myResourceGroup"
	-VirtualNetworkName "myVnet"
	- -OperatingSystem "win2016datacenter"

You have several VMs deployed in a Resource Group headed as “myResourceGroup”.
You plan to list every VM’s location by using PowerShell.
Considering this scenario, how should you complete the script below?
$VMs = Get-AzVM -ResourceGroupName MyResourceGroup
Foreach ($vm in $vms) {

[…]

}
	?$vm.Location
	- $vm.config.Location
	$vm.HardwareType.Location

You have an application named Application1. Your on-premise network hosts the web service that your Application1 consumes. You decide to deploy Application1 by creating an Azure App Service.
Considering this scenario, what app service plans are suited to host Application1?
	- Basic
	Premium
	Standard
	Free