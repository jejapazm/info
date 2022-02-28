### Crear usuario
```js
// seleccionar una base de datos como auth db
use admin
// crear el usuario
db.createUser({
    user:"analytics",
    pwd:"k8s@!jaef**R44",
    roles:[
        {role:"read", db:"inventory"},
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
    {
        roles:[
            {role:"read",db:"inventory"},
            {role:"read",db:"clients"}
        ]
    }
)
```
