cmdlet
	A powershell command is called cmdlet
	Each cmdlet should have a help file. Access it with the Get-Help cmdlet:
		`Get-Help Get-ChildItem -detailed`
Module
	cmdlets are shipped in modules.  A powershelll module is a dll
	List available modules:
		`Get-Module`
	
	
Define variables con $
	`$file = "C:\Users\fvarela\OneDrive - Siemens Healthineers\Documents\projects\trabajo\protons\extract_logs\test\mcs_logs\1673996750_OrionManager_HCYP010_2023-01-18TR1_20230117121015_1.log"`

Extrae texto de un fichero
	Todo el texto
		`Get-content $file`
	Solo ciertas líneas en base a un regex:
		`$m= Get-content $file | select-string -Pattern "Setting status flag (?<flag>.*) to 1"`
	Acceder al campo extraido en el primer match:
		`$m.matches[0].groups["flag"].value`
	Acceder a todos ellos en bucle
		`$m.Matches | foreach {$_.groups["flag"].value}`
	Extraer valores únicos:
		`$m.Matches | foreach {$_.groups["flag"].value} | Sort-Object | Get-Unique`

	
