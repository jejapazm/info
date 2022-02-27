
### Operaciones CRUD

### Insertar

```js
> db.inventory.insertOne(
{
    name: 'Duracell - AAA Batteries (4-Pack)',
    type: 'HardGood',
    price: 5.49,
    category: [
      { id: 'pcmcat312300050015', name: 'Connected Home & Housewares' },
      { id: 'pcmcat248700050021', name: 'Housewares' },
      { id: 'pcmcat303600050001', name: 'Household Batteries' },
      { id: 'abcat0208002', name: 'Alkaline Batteries' }
    ],
    manufacturer: 'Duracell',
    model: 'MN2400B4Z'
  }
)
> db.products.insertOne({name: "laptop", price: 100})
> db.products.insertMany({name: "laptop", price: 100},{name: "headphones", price: 30},{name: "mouse", price: 20})
```

### actualizar

```js
> db.products.updateOne({_id: ObjectId('65sad7s6f58a8766a8')},{$set: {price: 200}})
> db.products.updateMany({_id: ObjectId('65sad7s6f58a8766a8')},{$set: {price: 200}})
> db.products.updateMany(
    {}, 
    {
        $set:{"client_name":"grupo quirola"} 
    }, 
    {upsert:false, multi:true}
)
```

### Eliminar

```js
> db.products.deleteOne({price: {$lte: 75}}) # borra el primer documento que cumple la condicion
> db.products.deleteMany({price: {$lte: 75}}) # borra los documentos qu cumplen
```

### Buscar
```js
> db.products.findOne()  # devuelve un documento por orden natural
> db.products.findOne({name: "laptop"}) # duvuelve los que coincidan con la igualdad
> db.products.find() # devuelve todos
> db.products.findOne({name: "laptop", price: {$lte: 100}})  # operador and se especifica con comas # $lte operador menor que

> db.products.find({name: "laptop"}).count() # count da el numero de documentos que cumplenla condicion

```
