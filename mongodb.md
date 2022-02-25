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

### Operaciones CRUD
```js
// Insertar
> db.products.insertOne({name: "laptop", price: 100})
> db.products.insertMany({name: "laptop", price: 100},{name: "headphones", price: 30},{name: "mouse", price: 20})

// Actualizar
> db.products.updateOne({_id: ObjectId('65sad7s6f58a8766a8')},{$set: {price: 200}})
> db.products.updateMany({_id: ObjectId('65sad7s6f58a8766a8')},{$set: {price: 200}})
> db.products.updateMany(
    {}, 
    {
        $set:{"client_name":"grupo quirola"} 
    }, 
    {upsert:false, multi:true}
)


// Eliminar 
> db.products.deleteOne({price: {$lte: 75}}) # borra el primer documento que cumple la condicion
> db.products.deleteMany({price: {$lte: 75}}) # borra los documentos qu cumplen

// buscar
> db.products.findOne()  # devuelve un documento por orden natural
> db.products.findOne({name: "laptop"}) # duvuelve los que coincidan con la igualdad
> db.products.find() # devuelve todos
> db.products.findOne({name: "laptop", price: {$lte: 100}})  # operador and se especifica con comas # $lte operador menor que

> db.products.find({name: "laptop"}).count() # count da el numero de documentos que cumplenla condicion

# pedir ayuda
> db.inventory.help()
> db.help()

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
