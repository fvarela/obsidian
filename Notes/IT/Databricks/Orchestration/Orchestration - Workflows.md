Include a child notebook with %run
`%run "../includes/configuration"`

Notebook workflows
` v_results = dbutils.notebook.run("1.ingest_circuits_file", 0, {"p_data_source":"Ergast API"}`
Then in the notebook `1.ingest_circuits_file` add a 'return' statement like the following
`dbutils.notebook.exit("Success")`
'Sucess' would be assigned to v_results




