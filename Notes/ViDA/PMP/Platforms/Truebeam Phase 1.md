### Estimated time save in phase 1
TBD

### Current Tasks Review

5.2 Creating the initial PMP Machine File
	FV:
		Where is this getting the machine data?
		Can we streamline this so that it is not necessary to create the record the first time (If the record does not exist it creates it automatically without user intervention)

5.5 Uploading the PMP Machine File and PMP Checklist After a PMP Visit
	FV.
		We can upload the checklist to our cloud now and save time.

7.3 Analyze/Compare Data in the HET PMI Application
	FV.
		We can do the comparation in the app and make it better than it currently is.

21.13 Compare MVD, KVD and KVS Reference Positions
	FV.
		We have that info already on the PMI.wox file. We can remove this task

22.2.1 Capture Waveforms
	FV.
		We can automatically ingest the pdf file.
		Warning. We probably don't want to ingest just everything. 
		Perhaps manual upload of this file is good for now

23.1 Finalize HET PMI Program
	FV.
		That generates the `PMI.wox` file we need
		This task has to be performed first, when the initial data is gathered.
		No need to manually upload the file as we can get it with DDF.

23.6 Backup Nodes, Systems, Preference Settings
	FV.
		This is a manual check that a file was generated ok. We can skip this and check that a file exists automatically with DDF.

23.7 Managed Saved Parameter Data
	FV.
		The target files can be monitored by DDF and automatically uploaded to ViDA cloud.
		If we are ingesting the files with DDF do we still need them on the service computer?
		If we do need the files on the service computer. Can we move the files with DDF (or other tool)?

23.8 Distribute Official PMP Checklist
	FV.
		Can we skip saving the checklist and parameters on the service workstation and FSE computer if we have them in the ViDA cloud?
		Can the file upload to GCS be automatized? Is that regulatory? Isn't it enough to have the file in the cloud?

