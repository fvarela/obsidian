Azure Security Center
	Da un secure score
	Monitor service that provides threat protection across all of your services, both Azure and on-premises
	Features
		Just in time VM access
		Adaptive application controls
		Analyze and identify inbound attacks
		Use machine learning
		File integriting monitoring
	Two tiers
		Free
			Security policies
			Assessments
			Recommendations
		Standard
			Robust set of features including threat intelligence

Azure Sentinel
Creates a single report that show all security information.
	SIEM System (Security Information and Event Management)
	Collects data
	Detect threats
	Investigate threats with AI
	Respond to incidents

Key vault
	Manage secrets
	Manage encryption keys
	Manage SSL/TLS certifications
	Store secrets backed by hardware security modules (HSMs)
	Key vault
	Key vaults enable you to control and log access to anything stored in them.
	Cada vault es como una carpeta dentro de un sistema de ficheros
	Your app does not have direct access to the key in the key vault. They can only access the key by calling cryptography methods in the key vault
	Access to key vault
		You have to be authorized. There is no public access to key vaults.
		Roles
			Key vault contributor
				Recommended
				Allows access
			Contributor
				Full admin rights
		There are other 'access policy' for reading and writing data in Key Vault.
		Restrict network access as much as possible
	Components
		Certificates
		Keys
			Keys can be single instance or versioned
			Keys can be hardware protected or software protected.
				Hardware Security Modules (HSM)	
					Recommended for production
				Software Protected Keys
					Provide almost the same features as HSM
					Good for development
		Secrets
			Small data blobs >10kb protected by HSM
			Secrets exists to store sensitive data that almost every application has.
Digital data always exists in one of these three stages:
	At rest
	In process
	In transit

Data at rest
	Should be encrypted
	First apply Microsoft disk encryption
		Combined Bit-Locker and Linux DM-Crypt feature
	Azure Storage and Azure SQL DB encrypt data at rest by default.

Data in process.
	Try to use always SSL/TLS, HTTPS protocols
	Use VPN to isolate the communications channel between premises and cloud.
	Use Azure VPN Gateway to send encrypted traffic between on prem and Azure Virtual net.
	Access from on prem individual ws to Azure Virtual Net use point-to-site vpn
	To move large datasets over a dedicated high speed WAN link use Azure ExpressRoute
	If you use ExpressRoute you can also encrypt data at the application by using SSL/TLS
	Whe interacting with the Azure Storage from the Azure Portal all the comm is HTTPS

 Data discovery and classification is a set of features built into Azure SQL Database. They try to protect the data not only at rest (when saved in the db). 
	 Discovers data. Looks for potencially sensitive information
	 Labelling. Apply labels to data
	 Query. The query results set sensitivity in real time

Data in transit
	Use HTTPS
	
Secure Azure Storage Account
	By default all data is encrypted at rest
	It the secure transfer option is enabled you can enforce to use HTTP to transfer data
	Access can be managed with access keys or shared access signatures
	Access can be managed with Role Based Access Control or Active Directory
	You can audit the Azure Storage Account with the built in analytics.

Virtual Machines HDs can be encrypted with Azure Disk Encryption:
	BitLocker for Windows images
	DM-Crypt for Windows

CORS
	Cross Origin Resource Sharing
	This support is an optional flag you can enable on storage account.

RBAC
	Role based access control
	You can assign roles that are scoped to:
		Subscription
		Resource group
		Storage account
		Container or queue
	To create a role you need three things:
		Security principal (who)
		Scope (where)
			works in a parent-child way. If you have access to a parent you have access to all children beneath. 
				Management group > Susbscription > Resource group > Resource
		Role definition (what you can do)
			Buit-in roles :
				owener
				contributor
				reader
				user access administrator

Storage account keys:
	The best solution for APPS that access blobs or queues is Active directory.
	For other apps you can use Shared key. This is the easiest to use and supports everything:
		Blobs
		Queues
		Files
		Tables
	The keys give access to everything in the account
	The account has only 2 keys
	To change keys:
		Modify all apps to use the secondary key
		Refresh the primary key
		Change all apps to use the primary key again
		Refresh the secondary key

Shared Access Signature
	You shouldn't share storage account keys with external third party apps.
	For untrust clients use Shared Access Signature (SAS)
		With SAS you only allow the access that the application needs to do the task

Network Access to a storage account
	By default the storage account accepts connection from clients on any network
	You can restrict to specific IP addresses, ranges, and virtual networks
	You can manage access rules with:
		Powershell, azure cli
		Azure portal

Azure Defender for storage:
	This is not free
	Allows you to detect threats
	The alerts are integrated in Azure security center and are sent via email
	This is available for blob storage, azure files, azure data lake storage gen2

Accounts with hierarchical name spaces enabled support transactions using both
	Azure blob storae APIs
	Data Lake storage APIs

Azure File shares support transactions over SMB

Azure Data Lake Storage Gen2
	It is build on Azure Blob Storage so supports the same security features
	Provides Access Control Lists (ACLs)
		Authenticate users through Azure Active Directory OAuth 2.0
	








