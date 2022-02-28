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

### Contar
```js
db.inventory.find({}).count()
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

