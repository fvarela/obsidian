
Peter's Sharepoint:
[SharePoint](https://healthineersnam-my.sharepoint.com/personal/peter_bearjar_varian_com/_layouts/15/onedrive.aspx?id=%2Fpersonal%2Fpeter%5Fbearjar%5Fvarian%5Fcom%2FDocuments%2FVarian%2FOSS%2FEmber%2Ftemp%2FViDA&ga=1)


- Each deployment has a number of executions that can be either finished or unfinished.

- Both Finished and Unfinished logs the same 'definitionId' (e.g: "v17_v18_ARIA_Eclipse_Deployment_1_4_236_01_323"). That value can be used as an id of the deployment. All the sites where this particular deployment was performed will have the same definitionId on all their executions
- A particular deployment run on a site (e.g. "v17_v18_ARIA_Eclipse_Deployment_1_4_236_01_32" on HIT0041M ) does not have any unique id generated that we can use to find that particular deployment run on that particular site. (I manually generated a key to solve this)
- Executions have steps, roles and variables. 
- Steps can be successful, failed or sipped
- An step has actions

old tables:
csv_ember_jobs
	csv_ember_deployments
		csv_ember_execution_finished
		csv_ember_execution_unfinished
			csv_ember_variables
			csv_ember_roles
			csv_ember_steps
				csv_ember_actions

new tables:
csv_ember_run
	csv_ember_variables
	csv_ember_roles
	csv_ember_steps
		csv_ember_actions




- TODO:
- Eliminar tabla csv_ember_jobs
- Eliminar table csv_ember_deployments
- Eliminar table csv_execution_finished
- Eliminar tabla csv_execution_unfinished

- Crear Tabla csv_ember_upgrade (sustituye csv_ember_jobs, deployments y executions):
	- Una línea por ejecución.
	- upgrade_id es común a todos los upgrades de ese tipo
	- Fields:
		- pcsn, upgrade_id, deployment_name, total_active_time, finished_runs, unfinished_runs, total_successful_steps, total_failed_steps, total_skipped_steps.

- cambiar execution_id a run_id en todas partes
- csv_ember_steps:
	- Añadir total_minutes.