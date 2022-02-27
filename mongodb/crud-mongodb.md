
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
