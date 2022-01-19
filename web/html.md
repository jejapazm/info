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







