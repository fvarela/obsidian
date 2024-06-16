
#### Database
Create
	Just type `use` and the name you want to use as database
```
use my_db
```

#### Collection

Create - Two options

1. Command `create collection`:
	```bash
db.createCollection("empleados")
```

2. Insert on a collection that does not exist.
```bash
db.ciudades.insertOne({nombre_ciudad: "Madrid"})
```

List collections
```bash
show collections
```


#### Documents

##### Insert
- Insert one
```bash
db.empleados.insertOne({
	nombre:"Pedro",
	apellidos : "Rodriguez",
	edad: 30,
	aficiones: ["paracaidismo", "lectura", "fútbol"]
	})
```

When you run that the shell returns the object id `isertedId: ObjectId("6463a90....")`

- Insert specifying the id:

Be careful when doing this as all the 'id' have to be unique.

```bash
db.empleados.insertOne({_id: 1, nombre:"Rose"})
```



- Insert many
```
db.empleados.insertMany
```