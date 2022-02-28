
### Operaciones CRUD

### Insertar

```js
// Insertar uno
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
// Insertar varios
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

### Actualizar

```js
// Actualizar uno
> db.inventory.updateOne(
  {_id: ObjectId("621c0d2c9731244904a33890")},
  {
    $set: {"name":"Duracell - AAA Batteries (12-Pack)"}
  }
)
// Actualizar varios
> db.inventory.updateMany(
  {"type": 'HardGood'},
  {
    $set: {"type":"Hard-Good"}
  }
  {upsert:false, multi:true}
)
// Quitar propiedades con $unset
b.records.update(
  {},
  {
      $unset:{"client_name":"grupo quirola"}
  },
  {upsert:false, multi:true}
)
```

### Eliminar

```js
// Eliminar uno
> db.inventory.updateOne(
  {_id: ObjectId("621c0d2c9731244904a33890")}
)
// Eliminar varios
> db.inventory.updateMany(
  {"type": 'HardGood'},
)
```

### Buscar
```js
// Devolver un documento por orden natural
> db.inventory.findOne()
// Devolver un documento por orden natural que coincida con el filtro
> db.inventory.findOne(
  {"type": 'HardGood'}
)
// Devolver varios
> db.inventory.find(
  {"type":"Hard-Good"}
)
// Devolver todos
> db.inventory.find()
```
