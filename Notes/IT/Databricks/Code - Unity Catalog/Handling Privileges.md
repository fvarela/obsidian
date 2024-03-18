### Inherited by ownership vs Manual privileges

__Inherited by ownership:__
* Databricks Administrator - Can access all objects in the catalog and the underlying filesystem
* Catalog owner - All objects in the catalog
* Database owner - All objects in the database.
* Table owner - Only the table
* .... (Similar rules apply to Views and Functions)

__Manual Privileges__
You can Use the SQL Editor (or notebooks) to handle theset. You can also do it from the Data Tab.

- Grant
- Deny
- Revoke

`GRANT <Privilege> ON <Object> <Object-Name> TO <user or group>`

- Action:
	- GRANT
	- DENY
	- REVOKE
	- SHOW GRANTS

- Privilege (some of them only):
	- SELECT - Read access to an object.
	- MODIFY - Add, Delete and Modify data to or from an object.
	- CREATE - Create and object
	- READ FILES
	- WRITE FILES
	- EXECUTE (user defined functions)
	- ALL PRIVILEGES - Gives all privileges

* Objects:
	* CATALOG - Controls access to the entire data catalog
	* SCHEMA - Controls access to a database.
	* TABLE - Controls access to a managed or external table.
	* VIEW - Controls access to SQL views.
	* FUNCTION - Controls access to a named function.
	* VOLUME - Controls access to volumes
	* EXTERNAL LOCATION - Control access to external locations.
	* ANY FILE - Controls access to the underlying filesystem.

Examples:
- Grant 'USE CATALOG' privilege on the catalog 'dev' to group 'scholarnest-dev' group
```sql
GRANT USE CATALOG ON CATALOG dev TO `scholernest-dev`;
```
- Gran 'ALL PRIVILGES' on  the database demo_db:
```sql
GRANT ALL PRIVILEGES ON DATABASE dev.demo_db TO `scholernest-dev`;
```
* Grant read files permission to an external location:
```sql
GRANT READ FILES ON EXTERNAL LOCATION `external-data` TO `scholernest-dev`;
```

* Grant permissions on table
```sql
GRANT SELECT, MODIFY, READ_METADATA ON TABLE my_table TO user1@company.com
```

