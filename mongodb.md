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


### Operadores de comparación

| Nombre        | Descripción                    |
| -----------   |    -----------                 |
| $eq  | =  |
| $gt  | >  |
| $gte | >= |
| $lt  | <  |
| $lte | <= |
| $ne  | != |
| $in  | valores que están dentro de un arreglo |
| $nin | valores que no están dentro de un arreglo |


### Operadores de lógicos

| Nombre      | Descripción                    |
| ----------- |    -----------                 |
| $and (,)    | and  |
| $not        | not  |
| $nor        | nor  |
| $or         | or   |

### Operadores por elementos

| Nombre      | Descripción                    |
| ----------- |    -----------                 |
| $exist      | Documentos que cuentan con un campo específico             |
| $type       | Documentos que cuentan con un campo de un tipo específico  |

### Operadores para arreglos

| Nombre        | Descripción                    |
| -----------   |    -----------                 |
| $all          | Arreglos que contengan todos los elementos del query                        |
| $elemMatch    | Documentos que cumplen la condición del $elemMatch en uno de sus elementos  |
| $size         | Dcoumentos que contienen un campo tipo arreglo de un tamaño específico      |

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
