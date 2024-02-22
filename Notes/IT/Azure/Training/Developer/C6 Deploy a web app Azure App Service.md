Mean web:
	MongoDB
		Json like documents
		Available editions:
			Community server
			Enterprise server
			MongoDB atlas
	Express
	AngularJS
	Node.js

Deployment Slots (Web apps)
	Help with the testing and rollout
	Each slot has a different host name and is a different instance of the web app
	One slot is the Production slot
	Against these slots you can run tests such as :
		Integration tests
		Acceptance tests
		Capacity tests
	A slot swap is instantaneously. (It changes the configuration between the slots)
		If you want to use a staging database always with the staging version you can configure the connection to the database as a slot configuration.
	The slots share the resources of the App Service Plan
	Avoid Cold Start by using slot swaps. When you swap a slot into production you warm uup the app
	Slots are only available in:
		Standard tier
		Premium tier
		Isolated tier
	when creating a new slot you can copy the settings from other slot but not the content.
	You can limit the range of IP addresses that have access to the website in a slot

App Service Plans Tiers
	Free
	Shared
	Basic (up to 3 instances)
	Standard (up to 10)
	Premium (up to 30)
	Isolated (up to 100)

Scale a web app manually
	A web app can have multiple instances. Each instance runs on a virtual machine.
	The app service plan specifies the OS (Windows or Linux), the hardware, memory, etc
	When there are more than one app in an App Service Plan they will scale together. They need to have the same scaling requirements.
	Scale out: Add more instances up to the level of your selected tier
	When to scale up? Monitor:
		CPU utilization
		Memory occupancy
		Disk queue length
	
	
	
	