
### Estimated time save in phase 1
TBD

### Tasks review (Truebeam)

21.1  Collect XI Diagnostic Data		
	21.1.1. MV Test Imaging Chain
		FV: Can we automate the manual check of image data?
		==Yes==
	21.1.2. kV Test Imaging Chain
		FV: Can we automate the manual check of image data?
	21.1.3.1 Tube Calibration
		FV: The tube has to be calibrated every year. Can we move this to a regular task on the checklist?
		==We need the date when the tube is calibrated ->Combined / .bin / generator diagnostics==
		==Can be moved to a regular PMP task==
	21.1.4 Review EMD X-ray Generator Logs
		FV: Do we see any value in automating this?
		==Check fans fault, arcs, total number of exposures, temperatures, etc==
	21.1.5 Test Imaging Network
		FV: Do we see any value in automating this?
		
21.11 Record Norm Chamber Values
	FV: If we can add the image to the `.session` file we can automatically extract the `DNC Raw ADC Counts` 

21.11.3 X-Ray Generator Output Norm Chamber Readings
	FV: If we can add these images to the `.session` we can extract the norm chamber reading automatically.

21.13 Compare MVD, KVD and KVS Reference Positions
	FV. We have this info in the `PMI.wox` file so we may not need to generate the events

26.5 Measure Generator Output
	FV. Is there anything we can do with this


### Tasks review (Halcyon) - Only differences with TB

9.7 Generator Power ON and Inspect Cooling Fans
	FV. This one is linked with the step 'Review EMD X-ray Generator Logs'
	FV. (7280 - Fan Current Out of Range)
