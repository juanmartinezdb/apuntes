# CSS - Inserción de Estilos

## Tipos de Inserción de Estilos en CSS
En CSS, existen varias formas de insertar estilos para aplicarlos a los elementos HTML. Estos métodos permiten definir cómo queremos que se vea nuestra página web. A continuación, exploramos los principales métodos:

### 1. Inserción Interna
Este método se usa cuando queremos agregar los estilos directamente dentro de un documento HTML, más específicamente en la sección `<head>`. Para ello, utilizamos la etiqueta `<style>`.

```html
<head>
  <style type="text/css">
    body {
      color: white;
      background-color: green;
    }
  </style>
</head>
```
- **Nota**: Aquí definimos los estilos de manera interna para los elementos de la página, sin tener que crear un archivo CSS separado.
- También se puede importar un archivo CSS con `@import`:

```css
@import url("fich.css");
```

### 2. Inserción Externa
Otra forma de insertar estilos es utilizando un archivo externo CSS. Esta es la forma más común, ya que nos permite tener un archivo de estilos separado, lo cual mejora la organización y el mantenimiento del código.

```html
<link rel="stylesheet" href="fich.css" type="text/css" />
```
- **Ventaja**: Permite que múltiples páginas HTML compartan el mismo archivo CSS, facilitando la consistencia de estilos en toda la web.

### 3. Comentarios en CSS
Los comentarios en CSS se usan para añadir notas o explicaciones sobre el código. Los comentarios no afectan el funcionamiento de los estilos y se ignoran al renderizar la página.

```css
/**
 * Este es un comentario en CSS
 * que puede abarcar varias líneas
 */
```

## Ejemplo Básico de Estilos
Podemos definir estilos básicos para los elementos HTML de la siguiente manera:

```css
body {
  color: white;
  background-color: green;
}
```
En este ejemplo, el color del texto es blanco y el fondo es verde.

## Estilos mediante Atributos
Podemos aplicar estilos a elementos HTML utilizando atributos específicos como `class` e `id`. Ambos métodos tienen diferentes propósitos y prioridades:

### 1. Usando la Propiedad `class`
Podemos aplicar estilos a múltiples elementos usando `class`. Para definir los estilos relacionados a una clase, se utiliza un punto (`.`) seguido del nombre de la clase.

```html
<p class="parrafo">Este es un párrafo.</p>
```
```css
.parrafo {
  color: blue;
}
```
- **Nota**: Usar `class` nos permite aplicar los mismos estilos a diferentes elementos HTML, haciendo que todos compartan la misma apariencia.

### 2. Usando la Propiedad `id`
El atributo `id` se usa para aplicar estilos a un elemento específico. Al definir estilos para un `id`, se usa una almohadilla (`#`) seguida del nombre del `id`.

```html
<p id="parrafo-unico">Este es un párrafo único.</p>
```
```css
#parrafo-unico {
  color: red;
}
```
- **Nota**: `id` tiene mayor prioridad que `class` cuando hay un conflicto de estilos.

---
# CSS - Modelo de Caja

El modelo de caja en CSS es fundamental para comprender cómo se estructuran y visualizan los elementos en una página web. Cada elemento HTML se representa como una caja rectangular con varias propiedades importantes.

## Relleno (Padding) y Borde

### Propiedad `padding`
El **relleno** (`padding`) es el espacio entre el contenido del elemento y su borde. Podemos especificar valores para cada lado de la caja de diferentes formas:

- **Valores Simplificados**: Si queremos definir el relleno para los lados superior e inferior y los lados derecho e izquierdo:
  ```css
  padding: 2px 1px; /* 2px arriba y abajo, 1px derecha e izquierda */
  ```
- **Valores Individuales**: Si queremos definir el relleno de cada lado por separado:
  ```css
  padding: 2px 1px 2px 1px; /* top, right, bottom, left */
  ```

## Propiedades Comunes para `<p>`, `<div>` y `<span>`

- **`width`**: Define el ancho del elemento.
- **`background-color`**: Color de fondo del elemento.
- **`border`**: Define un borde alrededor del elemento. Puede ser sólido, punteado o discontinuo.
  ```css
  border: 2px dotted blue;
  ```
- **`margin-left` y `margin-right`**: Define el margen a la izquierda y derecha del elemento.
  - Si se usa `auto` en ambos márgenes, el elemento se centrará horizontalmente.

## Maquetación con `<div>` y Estilos
El elemento `<div>` ocupa por defecto todo el ancho de la página. Podemos posicionarlo para dividir la página sin usar tablas.

### Posicionamiento
Podemos posicionar un `<div>` usando las propiedades `top`, `left`, `bottom` y `right` junto con la propiedad `position`:

- **`static`**: El elemento sigue el flujo normal del documento.
- **`absolute`**: El elemento se posiciona en un lugar específico dentro de su contenedor.
- **`fixed`**: El elemento se mantiene fijo en la pantalla, incluso al desplazarse por la página.
- **`relative`**: El elemento se posiciona relativo a su posición original.

### Añadir una Caja Nueva
Podemos usar `float` para alinear cajas a la izquierda o derecha:

```css
float: right; /* Alinea el elemento a la derecha */
```
Para limpiar la flotación en un pie de página, utilizamos:

```css
clear: both;
```
Para centrar cajas, podemos agruparlas dentro de un único `<div>` y aplicar la siguiente propiedad:

```css
margin: 0 auto;
```

## Diseño de una Web

### Tamaños Fijos vs Diseño Líquido
- **Tamaños Fijos**: Un ancho fijo, por ejemplo, `800px`.
- **Diseño Líquido**: El diseño se adapta al tamaño de la pantalla usando propiedades como `float` y `clear`.

### Fondos
Podemos definir fondos para los elementos utilizando las siguientes propiedades:

- **`background-image`**: Define una imagen de fondo.
- **`background-position`**: Posiciona la imagen de fondo.
- **`background-repeat`**: Define si la imagen de fondo se repite o no.
- **`background-attachment`**: Define si la imagen de fondo se desplaza con la página o permanece fija.

### Estilos en Listas
Podemos aplicar estilos personalizados a listas:

```css
#lista {
  list-style: none;
}
#lista li {
  display: inline;
}
```
- **`list-style`**: Permite eliminar viñetas o números de las listas.
- **`display: inline`**: Alinea los elementos de la lista en línea con los demás elementos.

## Alinear Formularios sin Tablas
Para alinear formularios, podemos usar las siguientes etiquetas y propiedades:

- **`legend`**: Agrupa y añade un borde al formulario.
- **`fieldset`**: Agrupa los campos de un formulario.
- **`label`**: Etiqueta asociada a cada campo.

### Propiedades Útiles
- **`display: block`**: Hace que un elemento ocupe toda la línea.
- **`float: left/right`**: Alinea elementos a la izquierda o derecha.
- **`padding-right`**: Define el espacio interno a la derecha del elemento.

### Control de Visibilidad
Podemos hacer visibles o invisibles ciertos elementos basados en eventos:

```css
#activador:hover #soyinvisible {
  visibility: visible;
  display: block; /* Mostrar el elemento */
}
```

## Contenedores Flexibles (Flexbox)
Flexbox es una técnica moderna para definir contenedores flexibles, permitiendo diseñar elementos en una sola dimensión (fila o columna).

### Definir un Contenedor Flex
- **Contenedor Flex**: Para definir un contenedor flexible:
  ```css
  .contenedor-flex {
    display: flex;
  }
  ```
- **Elemento Inline Flex**: Los elementos ocupan solo el espacio necesario:
  ```css
  .contenedor-inline-flex {
    display: inline-flex;
  }
  ```

### Propiedades de Flexbox
- **`flex-wrap`**: Define cómo se comportan los elementos si no caben en el contenedor.
  - `nowrap`: Los elementos se reducirán para caber.
  - `wrap`: Los elementos mantendrán su tamaño y se moverán a una nueva línea si es necesario.

- **`justify-content`**: Justifica el contenido a lo largo del eje horizontal.
  - `flex-start`: Alinea los elementos al principio.
  - `flex-end`: Alinea los elementos al final.
  - `center`: Centra los elementos.
  - `space-between`: Distribuye los elementos con espacio entre ellos.
  - `space-around`: Distribuye los elementos con espacio alrededor.

- **`align-items`**: Alinea los elementos en el eje vertical.
  - `stretch`: Estira los elementos para llenar el contenedor.
  - `flex-start`, `flex-end`, `center`, `baseline`: Alinea los elementos de diferentes maneras.

```css
#container {
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
```

- **`flex-direction`**: Define la dirección de los elementos (`row`, `row-reverse`, `column`, `column-reverse`).

### Otras Propiedades de Flexbox
- **`flex-grow`**: Define cómo crecen los elementos en relación con otros.
- **`flex-shrink`**: Define si los elementos se encogen si no hay suficiente espacio.
- **`flex-basis`**: Tamaño inicial de la caja.
- **`order`**: Cambia el orden de los elementos.

```css
.flex-item {
  flex: 1 0 100px; /* flex-grow, flex-shrink, flex-basis */
}
```

---
# CSS - Variables, Efectos, Animaciones y Media Queries

## Variables CSS o Propiedades Personalizadas

Las **variables CSS** permiten definir valores reutilizables en diferentes partes de tu hoja de estilos. Estas variables se crean con dos guiones (`--`) y se suelen incluir en el pseudoelemento `:root` para tener un alcance global en el documento.

### Definición de Variables

```css
:root {
  --principal-color: black;
}
```
En este ejemplo, se define una variable llamada `--principal-color` con valor `black`.

### Uso de Variables
Para usar una variable personalizada, se utiliza la función `var()`:

```css
.clase {
  background-color: var(--principal-color);
}
```
De esta forma, podemos aplicar el color definido en la variable a cualquier elemento que tenga la clase `.clase`.

## Efectos CSS3

### Sombras
Podemos agregar **sombras** tanto a texto como a elementos de caja para mejorar la apariencia visual de nuestra página.

#### Sombras de Texto (`text-shadow`)
El formato para agregar sombras al texto es el siguiente:

```css
text-shadow: 2px 3px 0px hsla(140, 3%, 36%, 0.5);
```
- **Explicación**: Este ejemplo aplica una sombra al texto desplazada `2px` hacia la derecha y `3px` hacia abajo, con una opacidad del `50%`.
- Las sombras a la izquierda y hacia arriba se definen con valores negativos.
- Se pueden agregar sombras adicionales separándolas por comas.

#### Sombras en Cajas (`box-shadow`)
Para agregar sombras a una caja, se usa `box-shadow`:

```css
box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.5);
```
Este ejemplo aplica una sombra a una caja con un desplazamiento de `5px` hacia la derecha y hacia abajo, una difuminación de `10px` y una opacidad del `50%`.

### Fondos Múltiples
Podemos aplicar múltiples fondos a un elemento, especificando la posición y otras propiedades:

```css
main {
  background: url(../images/imag1.png) left no-repeat,
              url(../images/imag2.png) center no-repeat;
}
```
En este ejemplo, se aplican dos imágenes de fondo al elemento `<main>`, cada una con su propia posición.

## Gradientes

### Gradiente Lineal
Un **gradiente lineal** permite crear una transición de colores suave de una dirección a otra:

```css
background: linear-gradient(90deg, #ccc 0%, #222 50%, #fff 100%);
```
- **Explicación**: Este gradiente comienza con el color `#ccc` al `0%`, cambia a `#222` al `50%` y termina en `#fff` al `100%`.

### Gradiente Radial
Un **gradiente radial** parte de un punto central y se extiende hacia afuera:

```css
background: radial-gradient(circle, orange 72%, red 100%);
```
- **Explicación**: En este ejemplo, el gradiente parte del centro (`circle`) y se extiende desde `orange` al `72%` hasta `red` al `100%`.

### Gradientes Repetitivos
Podemos usar gradientes repetitivos para crear patrones:

```css
background: repeating-linear-gradient(90deg, #ccc 0px, hsla(0, 1%, 50%, 0.1) 5px);
```
Los gradientes repetitivos permiten crear patrones sin tener que usar imágenes pesadas.

## Transiciones

Las **transiciones** permiten animar cambios en las propiedades CSS durante un periodo de tiempo definido.

### Ejemplo Básico

```css
.clase:hover {
  transition: all 1s ease;
  font-size: 26pt;
}
```
- **Explicación**: Este ejemplo aplica una transición suave de `1s` a todos los cambios en el estado `hover`, aumentando el tamaño de la fuente.

### Propiedades de Transición
- **`transition-property`**: Define la propiedad que se va a animar.
- **`transition-duration`**: Duración de la transición.
- **`transition-timing-function`**: Función que define la velocidad (`ease`, `linear`, `ease-in`, `ease-out`).
- **`transition-delay`**: Retraso antes de que inicie la transición.

## Transformaciones
Las **transformaciones** permiten modificar la apariencia de un elemento con movimientos, giros, escalas y más.

### Ejemplos de Transformaciones
- **`scale`**: Cambia el tamaño del elemento.
  ```css
  transform: scale(0.5); /* Reduce el tamaño a la mitad */
  ```
- **`translate`**: Desplaza el elemento.
  ```css
  transform: translate(10px, 20px);
  ```
- **`rotate`**: Gira el elemento.
  ```css
  transform: rotate(25deg);
  ```
- **`skew`**: Distorsiona el elemento.
  ```css
  transform: skew(5deg, 10deg);
  ```

## Animaciones con `@keyframes`
Las **animaciones** permiten definir cambios complejos que ocurren en una secuencia de tiempo usando `@keyframes`.

### Definir una Animación con `@keyframes`

```css
@keyframes ejemplo {
  from {
    font-size: 10pt;
  }
  to {
    font-size: 20pt;
  }
}
```
Esta animación cambia el tamaño de la fuente de `10pt` a `20pt`.

### Aplicar la Animación

```css
.clase:hover {
  animation: ejemplo 2.5s infinite ease-in;
}
```
- **Explicación**: La animación se llama `ejemplo`, dura `2.5s`, se repite indefinidamente (`infinite`) y usa la función de velocidad `ease-in`.

## Formularios - Pseudo-Clases
Podemos utilizar **pseudo-clases** para controlar la apariencia de los elementos del formulario dependiendo de su estado.

### Pseudo-Clases Comunes
- **`:required`**: Indica que un campo es obligatorio.
- **`:focus`**: Aplica estilo cuando el campo está seleccionado.
- **`:valid`** y **`:invalid`**: Para campos que contienen datos válidos o inválidos.

## Media Queries
Las **media queries** permiten aplicar diferentes estilos dependiendo de las características del dispositivo (como el ancho de pantalla).

### Ejemplo de Media Query

```css
@media (max-width: 800px) {
  .sidebar {
    display: none;
  }
}
```
- **Explicación**: Esta regla oculta el elemento con la clase `.sidebar` en pantallas de hasta `800px` de ancho.

### Tipos de Medios
- **`all`**: Se aplica a todos los dispositivos.
- **`print`**: Se aplica al imprimir.
- **`screen`**: Se aplica a pantallas.
- **`speech`**: Se aplica a lectores de pantalla.

### Operadores Lógicos
- **`and`**, **`or`**, **`not`**: Se usan para combinar o excluir condiciones.

```css
@media (max-width: 800px) and (orientation: portrait) {
  /* Estilos para dispositivos en orientación vertical y con ancho máximo de 800px */
}
```

---
