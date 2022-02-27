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
