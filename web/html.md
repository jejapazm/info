## Headings y Paragrhaps
El texto mas relevante de la pagina web se define en un ```<h1>```, no usar dos o más ```<h1>``` ya que puede confundir al navegador sobre cual es el contenido más importante. Colocar etiquetas ```<h2>``` hasta ```<h6>``` considerando la importancia y estilo de los textos importantes. Para los textos menos importantes o información se puede usar ```<p>```


## Estructurar el HTML

| Etiqueta                  | Descripción                                                              |
| -----------               |    -----------                                                           |
| ```<header></header>```   | La parte superior que en muchos sitios web se repite                     |
| ```<footer></footer>```   | La parte inferior por lo general info de contacto y derechos reservados  |
| ```<nav></nav>```         | Menús de navegacion                                                      |
| ```<main></main>```       | Contenido principal                                                      |
| ```<section></section>``` | Seccionar. Regla: si el primer elemento hijo es un ```<h2>``` a ```<h6>``` generalmente va dentro de un ```<section>```, a menos que sea el ```<main>```  |
| ```<article></article>``` | Para un blog o sección de noticias                                       |
| ```<aside></aside>```     | Barras laterales a la derecha o izquierda                                |
| ```<div></div>```         | Cuando no se pueda usar ninguno de los anteriores                        |

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
descargar pronto cosas específicas para que el usuario las vea de inmediato
```html
<link rel="preload" href="css/styles.css" as="style">
<link rel="stylesheet" href="css/styles.css">
```
### px, em, rem

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
El navegador muestra el CSS de acuerdo con que tan específico es el selector. CSS es en cascada, pero no significa que si un selector aparece después será tomado en cuenta como el último, sino más bien su especificidad.

Misma especificidad (toma el último) 
```css
p {}
p {} /* se elige este por el orden*/

```
Diferente especificidad (se toma el de mayor especificidad)
```css
p.parrafo {}  /* se elige este */
p {}
```
Como provocar la mayor especificidad 
```css
p {
    color: red!important; /*no recomendado */
}
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

#### Pseudoselectores y Custom Properties
```css
:root {  /* custom properties */
    --blanco: #ffffff;
    --oscuro: #212121;
    --primario: #ffc107;
    --fuente-principal: 3.8rem;
}
.titulo {
    color: var(--blanco);
}
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
https://necolas.github.io/normalize.css/
```html
<link rel="preload" href="css/normalize.css" as="style">
<link rel="stylesheet" href="css/normalize.css">
```
Librería que normaliza la apariencia del css en los diferentes navegadores, se agrega como una hoja de estilos

#### Display
Todos los elementos HTML tienen un display block o display inline por default

| Selector                     | Descripción                                  |
| -----------                  |    -----------                               |
| ```display: block;```        | Elementos que se colocarán uno debajo de otro sin importar su tamaño o contenido. Ejm: parrados, headers, div |
| ```display: inline;```       | El siguiente elemento se posicionará a la derecha una vez que haya tomado todo el espacio que requiere: Ejm: a, img |
| ```display: flex;```         | Habilita flexbox, un modelo unidimensional. Tiene dos ejes: fila o columna |
| ```display: grid;```         | Habilita Grid, un modelo bidimensional |


#### Enfoques para escribir código CSS
##### BEM – Bloque, Elementos y Modificadores
El código tiene una clase para el bloque principal y luego se va describiendo cada elemento con una clase y una clase para sus modificadores
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
.text-center {}  /* para centrar el texto */
.color-red {} /* para color rojo */
.bg-blue {} /* fondo azul */
.p-2 {} /* padding de 2 */
```
#### Módulos
Se define el contenido principal y después se va seleccionando cada uno de los elementos html
```css
.card {}
.card h2 {}
.card img {}
```

### Responsing Web Design
Enfoque para que los diseños se adapten a las diferentes  interacciones del usuario y a la resolución que utilizan
##### Media Queries
```css
@media (min-width: 480px) {
    /* code */
}
@media (min-width: 768px) {
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
El tamaño de lo que se muestra en pantalla está delimitado por 4 cosas: el tamaño del contenido, tamaño de relleno (padding), tamaño del borde (border) y el margen (margin)
```css
/* apply a natural box layout model to all elements, but allowing components to change */
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
    position: relative;
}
.contenido-hero {
    position: absolute;
    background-color: red;
    height: 20px;
    width: 20px;
    right: 0;
    top: 0;
}
```
