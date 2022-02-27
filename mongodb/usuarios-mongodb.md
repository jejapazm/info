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
