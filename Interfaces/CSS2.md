# CSS Grid, Centrado, Scroll Snap y Cursores

## CSS Grid
**CSS Grid** es una técnica poderosa que permite maquetar contenido ajustándolo a rejillas configurables. A diferencia de Flexbox, CSS Grid es bidimensional, lo que significa que puedes trabajar con filas y columnas al mismo tiempo, facilitando una maquetación más compleja.

### Creación de un Contenedor Grid
Para empezar a usar CSS Grid, primero debemos definir un contenedor con `display: grid` o `display: inline-grid` (si queremos que el contenedor se comporte como un elemento en línea).

```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 10px 20px;
}
```
- **`grid-template-columns`**: Define cuántas columnas tendrá el contenedor y su tamaño. En este ejemplo, usamos `repeat(3, 1fr)` para crear tres columnas iguales.
- **`grid-gap`**: Establece el espaciado entre filas y columnas. En este caso, `10px` es el espaciado entre filas y `20px` entre columnas.

### Propiedades Comunes de CSS Grid
- **`grid-template-rows`**: Define la cantidad y el tamaño de las filas. Los tamaños pueden ser valores absolutos (`px`), porcentajes (`%`), o fracciones (`fr`).
  ```css
  grid-template-rows: auto 1fr 2fr;
  ```
- **`row-gap`** y **`column-gap`**: Establecen el espaciado entre filas y columnas, respectivamente.
  ```css
  row-gap: 15px;
  column-gap: 20px;
  ```

## Centrando Elementos
Hay múltiples maneras de centrar elementos en CSS dependiendo de su tipo y del contexto:

### Centrando con Flexbox
**Flexbox** es una opción ideal para centrar elementos horizontal y verticalmente:

```css
.contenedor-flex {
  display: flex;
  justify-content: center; /* Centra horizontalmente */
  align-items: center; /* Centra verticalmente */
}
```

### Centrando Texto
Para centrar solo el texto dentro de un elemento:

```css
.texto-centrado {
  text-align: center;
  line-height: 200px; /* Asegura que el texto esté centrado verticalmente si el contenedor tiene una altura fija */
}
```

### Centrando Imágenes con Posicionamiento Absoluto
Para centrar imágenes dentro de un contenedor con posicionamiento absoluto:

```css
div img {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  -webkit-transform: translate(-50%, -50%); /* Compatibilidad con navegadores antiguos */
}
```
- **Explicación**: `left: 50%` y `top: 50%` mueven el punto de referencia al centro del contenedor, mientras que `transform: translate(-50%, -50%)` ajusta la posición de la imagen para que quede perfectamente centrada.

### Centrando Elementos dentro de un Grid
Si usamos **CSS Grid**, podemos centrar elementos dentro del contenedor usando:

```css
.grid-item {
  display: grid;
  place-items: center; /* Centra el contenido horizontal y verticalmente */
}
```

### Centrando Absolutamente con Margen Negativo
Otra forma de centrar elementos es usando **posicionamiento absoluto** y ajustando los márgenes:

```css
.clase {
  position: absolute;
  top: 50%;
  left: 50%;
  margin-top: -50px; /* Ajusta la mitad de la altura del elemento */
  margin-left: -50px; /* Ajusta la mitad del ancho del elemento */
}
```

### Centrando Texto Verticalmente en un Contenedor
Podemos usar propiedades como `display: table-cell` para centrar texto verticalmente:

```css
div {
  height: 200px;
  width: 200px;
  display: inline-table;
}
p {
  display: table-cell;
  vertical-align: middle;
}
```

### Usar el Tamaño del Viewport
Para ajustar un elemento al tamaño completo de la ventana:

```css
.fullscreen {
  height: 100vh; /* Ocupa el 100% del alto del viewport */
}
```

## Scroll Snap
**Scroll Snap** permite un desplazamiento suave y organizado entre secciones de contenido, ideal para mejorar la experiencia de navegación.

### Scroll Snap en un Contenedor
Podemos definir un contenedor que tenga puntos de anclaje al desplazarse:

```css
.contenedor-scroll {
  scroll-snap-type: y mandatory; /* Desplazamiento en el eje vertical, obligatorio */
}
.seccion {
  scroll-snap-align: start; /* Alinea las secciones al inicio */
}
```
- **`scroll-snap-type`**: Define cómo se comporta el desplazamiento. Puede ser `x` (horizontal), `y` (vertical), `block`, o `inline`, seguido de `mandatory` (detenerse en los puntos de anclaje) o `proximity` (detenerse en el punto más cercano).
- **`scroll-snap-align`**: Define la alineación de los elementos hijos (`start`, `center`, `end`, `none`).

## Scroll Behavior
**Scroll Behavior** se usa para definir cómo se comporta el desplazamiento, especialmente cuando se utilizan anclas o enlaces internos.

```css
html {
  scroll-behavior: smooth; /* Desplazamiento suave en toda la página */
}
```
- **Valores**: `auto` (predeterminado) o `smooth` (suave).

## Cursores
La propiedad **`cursor`** nos permite cambiar el tipo de cursor cuando el usuario pasa el puntero sobre un elemento.

### Ejemplos de Tipos de Cursor
- **`cursor: pointer`**: Muestra un puntero (usualmente una mano) indicando que el elemento es clicable.

```css
elemento {
  cursor: pointer;
}
```
- **Otros tipos de cursor** incluyen:
  - `crosshair`: Muestra una cruz.
  - `help`: Indica que hay ayuda disponible.
  - `move`: Indica que el elemento se puede mover.
  - `progress`: Indica que se está realizando una acción en segundo plano.
  - `wait`: Indica que el usuario debe esperar.
  - `zoom-in` y `zoom-out`: Indican que el elemento se puede acercar o alejar.

------
# Media Queries, Efecto Parallax, Menús y Overflow

## Media Queries
**Media Queries** son una herramienta fundamental en CSS para crear diseños responsivos que se adapten a diferentes tamaños de pantalla y dispositivos. Utilizando `@media`, podemos definir estilos específicos para distintos contextos, como el ancho de la pantalla o la orientación del dispositivo.

### Ejemplo Básico de Media Query
Podemos aplicar estilos diferentes cuando el ancho de la pantalla sea menor o igual a `800px`:

```css
@media (max-width: 800px) {
  .sidebar {
    display: none;
  }
}
```
- **Explicación**: Este ejemplo oculta el elemento con la clase `.sidebar` en pantallas pequeñas.

### Tipos de Media
- **`all`**: Se aplica a todos los dispositivos.
- **`print`**: Se usa cuando se imprime la página.
- **`screen`**: Se usa en pantallas.
- **`speech`**: Para lectores de pantalla.

### Operadores Lógicos
Podemos combinar varias condiciones usando operadores lógicos como `and`, `or`, y `not`.

```css
@media (max-width: 800px) and (orientation: portrait) {
  /* Estilos para pantallas pequeñas en orientación vertical */
}
@media not screen and (color) {
  /* Estilos para dispositivos sin pantalla o sin colores */
}
```

### Mobile First vs. Desktop First
- **Mobile First**: Primero se diseña para dispositivos móviles y luego se aplican ajustes para pantallas más grandes.
  ```css
  @media (min-width: 600px) { /* Tablet */ }
  @media (min-width: 1024px) { /* Desktop */ }
  ```
- **Desktop First**: Primero se diseña para pantallas grandes y luego se aplican ajustes para dispositivos más pequeños.
  ```css
  @media (max-width: 1023px) and (min-width: 600px) { /* Tablet */ }
  @media (max-width: 599px) { /* Móvil */ }
  ```

### Problemas Comunes
- **Conflictos de Estilos**: Puede haber conflictos cuando las media queries coinciden, por ejemplo, una con un ancho mínimo y otra con un ancho máximo.
- **Prioridad**: En caso de conflicto, la última media query definida tiene prioridad.

## Efecto Parallax
El **efecto parallax** crea una sensación de profundidad al mover el fondo y el contenido a diferentes velocidades mientras el usuario hace scroll en la página. Esto se logra colocando el contenido en un contenedor con una imagen de fondo fija.

### Ejemplo de Parallax
HTML:
```html
<div class="contenedor">
  <div class="contenido">
    <p>Contenido</p>
  </div>
</div>
```
CSS:
```css
.contenedor {
  background-image: url('fondo.jpg');
  background-attachment: fixed; /* Imagen de fondo fija */
  background-position: center;
  background-size: cover;
  height: 100vh;
}
```
- **`background-attachment: fixed`**: Hace que el fondo se mantenga fijo mientras el contenido se desplaza, creando el efecto parallax.
- **`background-size: cover`**: Asegura que la imagen de fondo cubra todo el contenedor.

## Menú Horizontal
Podemos crear un menú horizontal usando una lista desordenada (`<ul>`) que contiene los elementos del menú.

### Ejemplo de Menú Horizontal
HTML:
```html
<header>
  <nav>
    <ul>
      <li><a href="#">Inicio</a></li>
      <li><a href="#">Acerca de</a></li>
    </ul>
  </nav>
</header>
```
CSS:
```css
nav ul {
  list-style: none; /* Quita las viñetas */
  padding: 0;
}
nav li {
  display: inline; /* Los elementos del menú se alinean horizontalmente */
  margin-right: 20px;
}
```

### Submenú Desplegable
Podemos agregar un submenú que se despliegue al pasar el cursor:

HTML:
```html
<li>
  <a href="#">Servicios</a>
  <ul id="submenu">
    <li><a href="#">Consultoría</a></li>
    <li><a href="#">Desarrollo</a></li>
  </ul>
</li>
```
CSS:
```css
#submenu {
  visibility: hidden;
  position: absolute;
}
li:hover ul#submenu {
  visibility: visible;
}
#submenu li {
  float: none;
}
```
- **Explicación**: El submenú (`#submenu`) está oculto por defecto (`visibility: hidden`) y se muestra (`visibility: visible`) cuando el usuario pasa el cursor sobre el elemento padre (`li:hover`).

### Menú con Flexbox
Podemos usar **Flexbox** para alinear el contenido del menú de manera más flexible:

```css
nav {
  display: flex;
  justify-content: space-between; /* Imagen o logo a la izquierda, menú a la derecha */
}
nav ul {
  display: flex;
  list-style: none;
}
nav li {
  flex-grow: 1; /* Ocupa el mismo espacio */
}
```

## Propiedad Overflow
La propiedad **`overflow`** controla cómo se muestra el contenido que se desborda de un contenedor.

### Valores de `overflow`
- **`visible`**: El contenido que se sale del contenedor es visible (valor por defecto).
- **`hidden`**: El contenido que se desborda se oculta.
- **`scroll`**: Se muestra una barra de desplazamiento para que el usuario pueda ver el contenido desbordado.
- **`auto`**: El navegador decide si muestra o no una barra de desplazamiento, dependiendo del contenido.

### Control del Desbordamiento Horizontal y Vertical
Podemos controlar el desbordamiento por separado usando **`overflow-x`** y **`overflow-y`**:

```css
div {
  overflow-x: hidden; /* Oculta el desbordamiento horizontal */
  overflow-y: scroll; /* Agrega scroll para el desbordamiento vertical */
}
```

--------------
# Iconos, Botones CSS, Migas de Pan y Tooltips

## Iconos
Los **iconos** son una excelente manera de mejorar la apariencia de una página web y facilitar la interacción del usuario. Los iconos son gráficos vectoriales escalables (SVG), lo que significa que se ven bien a cualquier resolución y tamaño de pantalla.

### Iconos de Google
**Material Icons** de Google son iconos vectoriales claros y consistentes. Podemos agregarlos a nuestro proyecto enlazando la hoja de estilos correspondiente en la sección `<head>` de nuestro documento HTML.

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
```

Luego, podemos usar los iconos utilizando las etiquetas `<i>` o `<span>` con la clase `material-icons`.

```html
<span class="material-icons">favorite</span>
```

### Personalización de Iconos
Podemos personalizar los iconos cambiando su tamaño, color y otros efectos con CSS:

```css
.icorazon {
  font-size: 48px;
  color: red;
}
```
Esto hace que el icono sea más grande y de color rojo.

### Iconos Variables
Los **iconos variables** permiten modificar ciertos atributos como el grosor (`weight`), la categoría, y el tamaño (`optical size`). Estos se encuentran en apartados como `Custom` en Google Icons.

## Botones CSS
Podemos diseñar botones atractivos usando CSS, añadiendo efectos visuales como degradados o transformaciones al pulsarlos.

### Ejemplo Básico de Botón
```css
.boton {
  width: 100%;
  display: block;
  padding: 10px;
  background-color: #008CBA;
  color: white;
  border: none;
  text-align: center;
  cursor: pointer;
}
```
- **`width: 100%`**: El botón ocupa el ancho total del contenedor.
- **`display: block`**: Hace que el botón sea un bloque completo.

### Botón con Degradado
Podemos usar un **degradado** para el fondo del botón:

```css
.boton-gradiente {
  background-image: linear-gradient(to right, #6a11cb, #2575fc);
  color: white;
}
```

### Efecto de Pulsación
Podemos agregar una animación al hacer clic, creando un efecto de **pulsación**:

```css
.pulsar {
  transition: transform 0.3s ease-in-out; /* Transición suave */
}
.pulsar:active {
  transform: scale(0.9); /* Se reduce ligeramente cuando se hace clic */
}
```

### Botones con Iconos
Para agregar **iconos a botones**, primero debemos incluir la hoja de estilos de **Font Awesome** en la sección `<head>` de nuestro HTML:

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
```
Luego, podemos definir los botones con los iconos predefinidos:

```html
<button class="boton1"><i class="fas fa-exclamation-circle"></i> Primary</button>
<button class="boton2"><i class="fas fa-exclamation-triangle"></i> Warning</button>
```
- **`<i class="fas fa-exclamation-circle"></i>`**: Agrega un icono de advertencia al botón.

## Migas de Pan (Breadcrumb)
Las **migas de pan** son una herramienta de navegación que permite al usuario saber dónde se encuentra en la estructura de la página. Generalmente, se representan como una lista de enlaces separados por un símbolo (por ejemplo, `/`).

### Ejemplo de Migas de Pan
HTML:
```html
<ul class="migas">
  <li><a href="#">Home</a></li>
  <li><a href="#">Contact</a></li>
</ul>
```
CSS:
```css
ul.migas {
  list-style: none;
  padding: 0;
}
ul.migas li {
  display: inline;
}
ul.migas li + li:before {
  content: "/\00a0"; /* Separador entre ítems */
}
```
- **Explicación**: El selector `li + li:before` añade un separador (`/`) antes de cada ítem de la lista, excepto el primero.

## Tooltip
Los **tooltips** son pequeñas ventanas emergentes que muestran información adicional al pasar el cursor sobre un elemento. Pueden ser útiles para mostrar descripciones o detalles sin sobrecargar el diseño.

### Ejemplo de Tooltip
HTML:
```html
<div class="caja">
  <span class="mje">Mensaje del tooltip</span>
  Mi elemento
</div>
```
CSS:
```css
.caja {
  position: relative;
  display: inline-block;
}
.mje {
  visibility: hidden;
  width: 120px;
  background-color: black;
  color: #fff;
  text-align: center;
  border-radius: 5px;
  padding: 5px;
  position: absolute;
  z-index: 1;
  bottom: 125%;
  left: 50%;
  margin-left: -60px;
  opacity: 0;
  transition: opacity 0.3s;
}
.caja:hover .mje {
  visibility: visible;
  opacity: 1;
}
```
- **Explicación**: El tooltip (`.mje`) está oculto por defecto (`visibility: hidden`). Cuando el usuario pasa el cursor sobre el elemento (`.caja:hover`), el tooltip se hace visible (`visibility: visible`) y aparece con una transición suave.

---
