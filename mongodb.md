# MONGO

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
