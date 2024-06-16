Governance is the process to maintain control over your applications and resources in Azure.
It involves:
	Determining your requirements
	Planning your initiatives
	Setting strategic principles


Tenant root group > Management groups > Subscriptions > Resource groups > Resources

The Tenant root group will always exist by default. It is only one.

### Management Groups
+ The **Tenant Root Group** will always be unique and at the top level.
+ You can have a hierarchy or Management Groups below the Tenant Root Group
+ The Management Group children are:
	+ Other Management Groups
	+ Subscriptions
+ You can assign RBAC based on the management group or based on the subscription.
	+ If applied on the Management Group level all the children will inherit them:
		+ Other Management Groups
		+ Subcriptions.
+ Best practices:
	+ Keep the Management Group hierarchy reasonable flat.
+ You can create different Management Groups based on:
	+ Geographical structure
	+ Production Management
	+ Sandbox Management
	+ Isolate Sensitive Information in a different management group

### Subscriptions
Next logic grouping level, below Management Groups.
When designing which subscriptions you need keep in mind the following:
- If you have several sibling Subscriptions and you apply the same RBAC to all of them perhaps you should group all that Subscriptions under the same Management Group and apply the RBAC at that level.
- You can set scale limits on the subscriptions
- Having different subscriptions make it easier to check billing and cost reporting.
- You can create a subscription for shared common services that everyone shares
- Networking:
	- A virtual network inside a subscription does not have access to the resources at a different subscription unless it is routed specifically. 
		- Resources are isolated from one subscription to another.

When to use different subscriptions:
- Workloads that require additional policies and role-base access control.
- Track costs for departments (create a subscription for each department)
- Different subscriptions for different environments.
	- These are often isolated from one another.

### Resource Groups
Next logic grouping level, below Subscriptions
- Group resources that share the same life cycle. Deleting the resource group deletes all the resources under it.
- Any RBAC applied to the Resource Group will be inherited by its resources.
- Use resource locks to protect individual resources from deletion or change.

- Resource tagging. Use naming and tagging standards to organize your resources and be able to checks costs, apply security, etc