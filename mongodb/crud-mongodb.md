
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
> db.products.insertMany(
  {
    name: 'IK Multimedia - iRig Stomp - Black',
    type: 'HardGood',
    price: 59.99,
    category: [
      { id: 'abcat0207000', name: 'Musical Instruments' },
      { id: 'abcat0208024', name: 'Musical Instrument Accessories' },
      { id: 'pcmcat152100050033', name: 'DJ Equipment Accessories' }
    ],
    manufacturer: 'IK Multimedia',
    model: 'IRIGSTOMPIN'
  },
  {
    name: 'Maytag - 25.6 Cu. Ft. Side-by-Side Refrigerator',
    type: 'HardGood',
    price: 1699.99,
    category: [
      { id: 'abcat0900000', name: 'Appliances' },
      { id: 'abcat0901000', name: 'Refrigerators' },
      { id: 'pcmcat367400050001', name: 'All Refrigerators' }
    ],
    manufacturer: 'Maytag',
    model: 'MSB26C6MDM'
  }
)
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
