### Estimated time save in phase 1
TBD

### Current Tasks Review

3.Halcyon Software version
	Note: We can get the versions from the `PMI.wox` file
	Note: We can use that info to automate things
	 ==YES==
6.3 Run XI diagnostic data
	- Image analysis (get mean pixel count, standard deviation). 
	- Review 7280 event log messages
	
6.4 Review MPC Data:
	Note. We can get the MPC results with DDF and automate all that.
	==Not because the pipeline might be broken== 
	Note. We can plot the trends on the new app
	Q. If we ingest the results file is it still necessary to take screenshots?
	==FV - Check what we already have == 
	

7.1 Perform the MPC.
	Q. In the proposed workflow that we have been discussing the data gather would be the first step. Can we move this to the beginning of the PMI? ==Customer has to perform MPC every day so perhaps we can skip it. PSE will see==
	Q. Do we need this data source or can we use APT instead. ==We don't have it==
	==Will be nice to have the results in the app==

9.9.1 SMC Signal Check
	Note. We may have all of that in the PMI.wox so manual comparation might not be necessary.
	Q. Can we automate this? ==Yes, but we need to check if the PMI.wox is complete==

9.9.2 Check the Stand DC Power Supplies Voltages
	Note. We have all those parameters in the PMI.wox file
	Q. Can we automate this? ==Same as before. Check PMI.wox==

9.9.3 Measure Vacion Pump Voltage
	Note. We have those parameters
	Q. Can we automate this
	
11.2 Backlash/Reproducibility and Leaf Nuts
	Note. The MPC is used as the baseline for this? ==We need MPC. No specific MLC test in SMC for this==

11.3 MLC Diagnostic Tests
	Note. We can ingest all the test results in the PMI.wox
	Once the PMI is finalized we can get new records from their respective folders.
	==We need to get the results of the tests from the records folder == 

15.1 Compare Waveforms
	Q. Should we provide a way to save the waveforms file in the app.
	==That would be good==

15.2 AFC Sweep
	Note: We can analyze the record automatically and show plots in the app. we can remove the excel part
	==It would be good. FV - Explore this == 

17.4 Managed Saved Parameter Data
	Note: We can save checklists and records on the cloud with DDF.
	Q. Are there any regulatory issue with keeping these files? 
	Q. Can we avoid moving files from Truebeam WS to Service WS?
	==We can probably avoid moving the files if we already have them in the cloud==




==Nice to have. Run the platform maintenance from the Service Workstation==