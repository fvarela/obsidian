

##### Maintenance Platform definition:

The solution is a single cloud- and __web-based__ application, device agnostic, built upon existing ViDA infrastructure, to host planned maintenance activities for Varian products, __interfaced with Salesforce__ to automatically connect contract entitlements with work orders and cases. __Digitally available information like machine performance data and parameter checks are automatically populated__. The documentation of activities is __automated__, e.g. case closure in Salesforce, upload and storage of documents.


##### Expected Internal benefits for Field Service Engineers and District Managers:

1. Ease of use thanks to connected data sources and information available when required.
2. Seamless access to pending tasks incl. instructions
3. Reduced admin workload thanks to automation
4. Monitoring of maintenance performance, gaps, improvement opportunities


#### Pain Points / Challenges for PMP on TrueBeam systems
-  Toolset
	- Multiple different tools (iSIR, ViDA, HET-Tool, C-Tool, Orion, Salesforce, GCS Data Center)
	- Time consuming and difficult to navigate to each one.
-  Determine Health of Machine
	- Logs are not sent to the FSE before they arrive on site
- Outdated Technology
	- Inflexible interface, Windows only.
- PMP Tasks Dashboard in HET-Tool
	- Not clear what tasks are overdue, what tasks need to done, etc
	- Not good for collaborative PMPs (PMP performed by more than one FSE)
- Identify unplanned / planned time
	- Unable to differentiate  planned vs unplanned time in WO
	- Due to this it is not clear the type of difficulties FSEs run into while doing the PMPs.
- Feedback Button
	- Not easy to provide feedback
	- No improvement cycle
	- Feedback not properly stored / channeled.
- Event log Review
	- To find the solution to error FSE need to search multiple platforms / documents.
- Admin Tasks
	- Tedious to identify the QA tasks the customer must perform after the PMP.
	- Upload PMP results to many different tools: HET, GCS data center, Salesforce
- Manual Data Entry
	- Manual Data Entry into multiple tools

Ref:
- Business Case: PLM CSS-129-Rev 01 Business Case PMP

##### Out of Scope
- Maintenance performed by Distributor FSEs
- Maintenance performed in a collaborative way between VAR and customer
- Maintenance performed by 3rd party
- Scheduling planned maintenance

Existing PMP-tools, e-g- HETTool needs to remain because it's used by customers and FSEs in case maintenance is shared.

##### Goal
For the initial release the goal is:
- __10 hour__ reductions in planned maintenance globally in FY26 due to automated and simplified workflow.
- __60%__ adoption rate on TB>=4.0 and Avalon.