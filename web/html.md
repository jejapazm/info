## Headings, Paraghraps
Se define el texto mas relevante con ```<h1>```, solo usar un ```<h1>``` en toda la página ya que puede confundir al navegador sobre cual es el contenido más importante. Colocar etiquetas ```<h2>``` hasta ```<h6>``` considerando la importancia y estilo de los textos importantes. Para los textos menos importantes o información usar ```<p>```

## Estructurar el HTML

| Etiqueta                  | Descripción                                                              |
| -----------               |    -----------                                                           |
| ```<header></header>```   | Parte superior que en muchos sitios web se repite                        |
| ```<footer></footer>```   | Parte inferior generalmente para info de contacto y derechos reservados  |
| ```<nav></nav>```         | Navegacion                                                               |
| ```<main></main>```       | Contenido principal                                                      |
| ```<section></section>``` | Secciones. Si el primer elemento hijo es ```<h2>``` a ```<h6>``` generalmente va dentro de un ```<section>```, a menos que sea el ```<main>```  |
| ```<article></article>``` | Para un blog o sección de noticias                                       |
| ```<aside></aside>```     | Barras laterales derecha o izquierda                                     |
| ```<div></div>```         | Cuando no se usa ninguno de los anteriores                               |

## Formularios
  
```html
<form action="">
    <fieldset>
        <legend>Contáctame</legend>
            <label for="name">Nombre</label>
            <input type="text" id="name" placeholder="tu nombre">
            <label for="telefono">Teléfono</label>
            <input type="tel" id="telefono" placeholder="tu teléfono">
            <label for="mail">Correo</label>
            <input type="email" id="mail" placeholder="tu correo">
            <label for="">Mensaje</label>
            <textarea name="" id="" cols="30" rows="10"></textarea>
            <input type="submit" value="Enviar">
    </fieldset>
</form>
```

# CSS

### Selectores

| Selector                      | Ejemplo                                      |
| -----------                   |    -----------                               |
| de Elemento                   | ```h1 {}```                                  |
| de Clase                      | ```.class-name {}```                         |
| de Id                         | ```#id-name {}```                            |
| Combinacion de descendientes  | ```h1 span {}```, ```class-name #id-name {}```, ```#id-name span {}```, ```.class-name1 .class-name2 {}``` |
| de Atributo                   | ```[src="logo.jpg"] {}```                    |
| Todos los hijos               | ```.class-name > p {}```                     |


### Preload
Para descargar pronto cosas específicas para que el usuario las vea de inmediato
```html
<link rel="preload" href="css/styles.css" as="style">
<link rel="stylesheet" href="css/styles.css">
```
### Medidas px, em, rem

#### Hack para unidades px y rem => 1rem = 10px
```css
html {
    font-size: 62.5%;
}
body {
    font-size: 16px;
}
```

#### Especificidad
El navegador muestra el CSS de acuerdo con que tan específico es el selector. Lo que significa que si un selector aparece después de otro igual no necesariamente este será tomado, sino más bien el que tenga mayor especificidad.

Misma especificidad (CSS toma el último) 
```css
p {}
p {} /* se elige este por el orden*/
```

Diferente especificidad (CSS toma el de mayor especificidad)
```css
p.parrafo {}  /* se elige este */
p {}
```

Provocar la mayor especificidad (no remomendado)
```css
p { color: red!important; }
```

#### Colores

Por nombre
```css
color: red
```
Hexadecimal #xxx #xxxxxx
```css
color: #212121
```
rgb o hsl
```css
color: rgb(red, green, blue)
```
rgba o hsla
```css
color: rgba(red, green, blue, alpha)
```

#### Pseudoselectores (:root) y Custom Properties
```css
:root {  
    --blanco: #ffffff;
    --oscuro: #212121;
    --primario: #ffc107;
    --fuente-principal: 3.8rem;
}
p { color: var(--blanco); }
```
#### Fuentes

https://fonts.google.com/
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Krub:wght@400;700&display=swap" rel="stylesheet">
```
```css
font-family: 'Krub', sans-serif;
```
#### Normalize CSS
Librería que normaliza el css en los diferentes navegadores.
```html
<link rel="preload" href="css/normalize.css" as="style">
<link rel="stylesheet" href="css/normalize.css">
```
https://necolas.github.io/normalize.css/

#### Propiedad Display
Todos los elementos HTML tienen un display block o display inline por default

| Selector                     | Descripción                                  |
| -----------                  |    -----------                               |
| ```display: block;```        | Elementos que se colocarán uno debajo de otro sin importar su tamaño o contenido |
| ```display: inline;```       | El siguiente elemento se posicionará a la derecha una vez que el primero haya tomado todo el espacio que requiere |
| ```display: flex;```         | Habilita flexbox, un modelo unidimensional |
| ```display: grid;```         | Habilita Grid, un modelo bidimensional |

#### Enfoques de escritura  CSS
##### BEM – Bloque, Elementos y Modificadores
Una clase para el bloque principal, varias clases con dos guiones bajos para los elementos y modificadores de elementos aumentando dos guines
```css
.card {} /*  bloque */
.card__titulo {} /* elementos */
.card__imagen {}
.card__boton {}
.card__boton--activate {} /* modificador */
```
##### Utility First
Se crean clases con una sola propiedad que describen que es lo que harían.
```css
.text-center { text-align: center; }
.color-red { color: red }
.bg-blue { backgound-color: blue; }
.p-2 { padding: 2rem; } 
```
#### Módulos
Se define el contenido principal y después se va seleccionando cada uno de los elementos html
```css
.card {}
.card h2 {}
.card img {}
```

### Responsing Web Design con Media Queries
Enfoque para que los diseños se adapten a las diferentes interacciones del usuario y resolución de pantalla que utilizan
```css
@media (min-width: 480px) {
    /* code */
}
```
##### Estándar en Media Queries
```
480px cambia cuando sea un teléfono
768px cambia cuando sea una tablet
1149px para laptop o desktop pc
1400px dispositivos más grandes
```

### Box Model
El tamaño de lo que se muestra en pantalla está delimitado por el tamaño: del contenido, del relleno (padding), del borde (border) y del margen (margin). 
#### Apply a natural box layout model to all elements, but allowing components to change
```css
html {
    box-sizing: border-box;
}
*, *:before, *:after {
    box-sizing: inherit;
}
```

### Posicionar elementos
```css
.hero {
    background-color: rosybrown;
    height: 45rem;
    width: 45rem;
    padding: 2rem;
    position: relative; /* <----- */
}
.contenido-hero {
    position: absolute; /* <----- */
    background-color: red;
    height: 20px;
    width: 20px;
    right: 0; /* <----- */
    top: 0; /* <----- */
}
```
