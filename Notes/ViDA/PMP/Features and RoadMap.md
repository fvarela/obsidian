
## General ideas:
- Create a new app to handle the maintenance of the machines. 
- Like **HETTOOL** but web based and supporting many platforms.
- It will leverage the power of **DDF** to ingest records in real time.
- It will have access to all the VIDA infrastructure and data. Past records, insights...
- It will integrate some functionalities that are currently spread across several tools/platforms:
	- iSir
	- Salesforce
	- GCS
	- Ctool
	- Hettool
	- ViDa

## PMP General Workflow
- Gather all the records first.
- The records are automatically uploaded, parsed and data is pushed to the app.
- FSE performs the PMP. Ideally only cleaning, greasing, etc as all the data has been collected already.

## Phase 1. Features

- Automate manual tasks as much as possible 
- Display Parameters in near real time:
	- Beginning of PMP. Create baseline
		- APT (Auto Performance Test)
		- Imager Diagnostic.
	- During PMP
		- TBD. Might be necessary to ingest other records in real time.
- Unity integration
##### I-Sir integration. (Currently in study)
- Access to GCS documentation
- Documents should be:
	- Unprotected (non hasp)
	- Up to date.
- We will need to access the network location programmatically like a shared folder, cloud storage, SharePoint, etc.
- What files? 
	- We can start by the PMP procedures for Halcyon and Truebeam
		- PMP-HT-Hettol-X.pdf
		- PMI-AL-X.pdf

![[Pasted image 20240614122740.png]]

## Phase 2. Features

- Review checklist task by task and make them data driven.
	- E.G. If the data says the gantry is fine do not grease it again.
	- To implement this we will define __three target dates__ for each task:
		1. Default target date
			- Same as always. Every 3, 6, 9 months, etc.
		2. Based on data target date
		3. Maximum date. 
			- No matter what the data says. Do this at least once every two years.
	- The logic could be something like:
		- The target date based on data (2) would overwrite the default one (1) if is value is less than the maximum date (3) since the last time the task was performed.

	

