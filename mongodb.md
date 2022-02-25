# MONGO

### Comandos básicos

```js
// Mostrar las bases de datos existentes
> show dbs
// Crear o usar una base de datos
> use <database-name>
// Mostrar la base de datos actual
> db
// Mostrar colecciones
> show collections
// Mostrar las colecciones de la base de datos actual
> db.getCollectionNames()
// Eliminar la base de datos actual
> db.dropDatabase()
```

### Proyecciones
```js
> db.inventory.findOne({Status: "A"})
{
    "_id": ObjectId("9o87asdf7076asd8f70776s8a70a"),
    "item": "journal",
    "status": "A",
    "size": {
        "h": 14,
        "w": 21,
        "oum": "cm"
    },
    "instock": [
        {
            "warehouse": "A",
            "qty": 5
        }
    ]
    
}
> db.inventory.findOne({status: "A"},{item:1, status:1})
{
    "_id": ObjectId("9o87asdf7076asd8f70776s8a70a"),
    "item": "journal",
    "status": "A",
}
```

### Tipo de datos
```
Strings		"Algun texto"
Boolean		True/False
ObjectId	ObjectId('3124ea5...')
Date		ISODate("2019-2-18T...")
Number
- Double
- Integer 32 bits
- Integer 64 bits
- Decimal
```

### Agregar campos en todos los documentos de una colección
```js
// Agregar
db.records.update(
    {},
    {
        $set:{"client_name":"grupo quirola"}
    },
    {
        upsert:false,
        multi:true
     }
)
// Quitar
b.records.update(
    {},
    {
        $unset:{"client_name":"grupo quirola"}
    },
    {
        upsert:false,
        multi:true
    }
)
```


### Crear usuario
```js
// seleccionar una base de datos como auth db
use admin
// crear el usuario
db.createUser({
    user:"analytics",
    pwd:"Pf%e_Q&etart@H7#",
    roles:[
        { role:"read", db:"mqtt_airscan" },
        { role:"read", db:"mqtt_aquascan" }
    ],
    passwordDigestor: "server"
})
```
### Eliminar usuario
```js
db.dropUser("analytics")
```

### Actualizar usuario
```js
db.updateUser(
    "analytics",
    {roles:
        [
            {role:"read",db:"mqtt_aquascan"},
            {role:"read",db:"mqtt_airscan"}
        ]
    }
)
```
