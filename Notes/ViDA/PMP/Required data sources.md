
### Required data sources. ==Draft!==

| Data source           | Truebeam | Halcyon | Exp. Freq | Workflow    | Level        |
| --------------------- | -------- | ------- | --------- | ----------- | ------------ |
| Finalized `PMI.wox`   | x        | x       | 4/y       | Prep        | Needed       |
| XI session `.session` | x        | x       | 4/y       | Prep        | Needed       |
| Waveforms `.pdf`      | x        | x       | 4/y       | Active      | Needed       |
| MPC results           | -        | x       | */y       | Prep/Finish | Nice to have |
| Service Records       | x        | x       | */y       | Prep/Active | Nice to have |

==Raysafe data. Saved locally for now. Support upload of this file==
==Motion records==
==bin files that contain the tube calibration==
==combined log. HU data, power supply==
==Inside the .session file 'get imager diagnostics' (later versions only)==


### Truebeam ==Draft!==
PMP beginning.
	User gathers all the initial necessary data 
	 `PMI.wox` - Populates general data on App
	 `.session` - Populates imaging data on App
PMP	 in process
	User runs service records on demand
		`service records` - Updates general data on App
PMP finish.
	No data requirement

### Halcyon. ==Draft!==
PMP beginning
	User gathers all the initial necessary data
		`PMI.wox` - Populates general data on App.
		`MPC result` - Populates MPC data on App.
		`.session` - Populates imaging data on App.
PMP in process
	User runs service records on demand
		`service records` - Updates general data on App
PMP finish
	User runs the MPC to make sure everything is fine
		`mpc` - Updates the MPC data on App

==Full PMI.wox requires desktop access!!==


