# Guía de CSS - Apuntes y Glosario

## Índice
1. [Inserción de Estilos](#inserción-de-estilos)
2. [Estilos mediante Atributos](#estilos-mediante-atributos)
3. [Pseudo-clases](#pseudo-clases)
4. [Selectores de Atributos](#selectores-de-atributos)
5. [Aplicación de Estilos y Preferencia](#aplicación-de-estilos-y-preferencia)
6. [Colores y Transparencia](#colores-y-transparencia)
1. [Modelo de Caja](#modelo-de-caja)
2. [Maquetación con `<div>` y Estilos](#maquetación-con-div-y-estilos)
3. [Contenedores Flexibles](#contenedores-flexibles)
4. [Variables CSS o Propiedades Personalizadas](#variables-css-o-propiedades-personalizadas)
5. [Efectos CSS3](#efectos-css3)
6. [Columnas y Tipografía](#columnas-y-tipografía)
7. [Estilos en Listas](#estilos-en-listas)
8. [Formularios y Estilos](#formularios-y-estilos)


---

## Inserción de Estilos

### Tipos de Inserción de Estilos en HTML

1. **Estilos Internos (`<style>`)**
   Los estilos se pueden insertar directamente dentro de la etiqueta `<head>` en HTML mediante una etiqueta `<style>`.
   ```html
   <style type="text/css">
     body { color: white; background-color: green; }
   </style>
   ```
   También se puede importar un archivo CSS externo usando `@import`:
   ```css
   @import url('fich.css');
   ```

2. **Estilos Externos (`<link>`)**
   También es posible incluir un archivo CSS externo mediante la etiqueta `<link>` en el `<head>`.
   ```html
   <link rel="stylesheet" href="fich.css" type="text/css" />
   ```

3. **Comentarios en CSS**
   En CSS, los comentarios se escriben usando `/* */`.
   ```css
   /* Este es un comentario en CSS */
   ```

## Estilos mediante Atributos

### Uso de `class` y `id` en los Estilos

- **`class`**: Permite aplicar el mismo estilo a múltiples elementos. Se define usando un punto (`.`) seguido del nombre de la clase.
  ```html
  <p class="parrafo">Texto del párrafo</p>
  ```
  En la hoja de estilos:
  ```css
  .parrafo {
    color: blue;
  }
  ```

- **`id`**: Se usa para identificar elementos únicos en una página y tiene prioridad sobre las clases. Se define usando una almohadilla (`#`) seguida del nombre del id.
  ```html
  <div id="contenedor">Contenido</div>
  ```
  En la hoja de estilos:
  ```css
  #contenedor {
    background-color: yellow;
  }
  ```

## Pseudo-clases

Las pseudo-clases permiten aplicar estilos a elementos en función de su estado. A continuación se enumeran algunas de las más comunes:

- **Pseudo-clases de enlaces**
  - `:link` - Aplica a los enlaces que no han sido visitados.
  - `:visited` - Aplica a los enlaces que han sido visitados.
  - `:hover` - Aplica cuando el usuario coloca el cursor sobre el elemento.
  - `:active` - Aplica cuando el enlace está siendo clicado.

  ```css
  a:link {
    font-size: 16pt;
  }
  a:hover {
    color: red;
  }
  ```

- **Pseudo-clases de formularios**
  - `:focus` - Aplica cuando un elemento, como un campo de formulario, tiene el foco del usuario.
  ```css
  input:focus {
    border: 2px solid blue;
  }
  ```

- **Pseudo-clases para párrafos**
  - `p:first-line` - Aplica estilo a la primera línea de un párrafo.
  - `p:first-letter` - Aplica estilo a la primera letra de un párrafo.

- **Pseudo-clases de elementos en cascada**
  - `:first-child` - Selecciona el primer hijo de un elemento padre.
  - `:last-child` - Selecciona el último hijo de un elemento padre.
  - `:nth-child(n)` - Selecciona el enésimo hijo, `odd` para impares, `even` para pares.
  ```css
  tbody tr:first-child {
    background-color: lawngreen;
  }
  ```
  - `:not(selector)` - Selecciona los elementos que no cumplen la condición especificada.

## Selectores de Atributos

Es posible aplicar estilos a elementos en función de sus atributos.

- **Selectores de Atributo Básicos**
  ```css
  a[title] {
    font-size: 16pt;
  }
  img[alt="logo"] {
    border: 1px dotted green;
  }
  ```

- **Selectores de Atributos con Caracteres Especiales**
  - `^=` - Selecciona elementos cuyo valor de atributo comienza con un valor específico.
  - `*=` - Selecciona elementos cuyo valor de atributo contiene un valor específico.
  - `$=` - Selecciona elementos cuyo valor de atributo termina con un valor específico.

  ```css
  a[href^="https"] {
    color: blue;
  }
  ```

## Aplicación de Estilos y Preferencia

### Combinación de Estilos
Cuando se aplican los mismos estilos a varios elementos, se pueden separar por comas.
```css
a, p, pre {
  color: black;
}
```

### Preferencia de Estilos en Conflicto
El orden de preferencia en CSS es el siguiente:
1. **Reglas aplicadas directamente en línea (`style`)** - Tienen la mayor prioridad.
2. **Hoja de Estilo Externa (`<link>`)** - Aplicada a través de un archivo externo.
3. **`@import`** - Las reglas importadas son las de menor prioridad.

Además, la declaración `!important` puede usarse para forzar la aplicación de una regla sobre cualquier otra.
```css
p {
  color: red !important;
}
```

## Colores y Transparencia

CSS permite definir colores de diferentes maneras:

- **Colores en Inglés**
  ```css
  color: red;
  ```
- **Colores Hexadecimales**
  ```css
  color: #ff0000;
  ```
- **RGB y RGBA**
  ```css
  color: rgb(255, 0, 0);
  color: rgba(255, 0, 0, 0.5); /* Transparencia con k entre 0 y 1 */
  ```
- **HSL y HSLA**
  ```css
  color: hsl(0, 100%, 50%);
  color: hsla(0, 100%, 50%, 0.5);
  ```

---

## Columnas y Tipografía

### Columnas

CSS permite la creación de columnas para organizar el contenido de manera más legible. Las siguientes propiedades ayudan a crear columnas de forma eficiente:

- **`column-count`**: Define el número de columnas en las que se dividirá el contenido.
- **`column-gap`**: Define el espacio entre las columnas.
- **`column-rule`**: Define una línea entre las columnas.

```css
.trescolumns {
  column-count: 3;
  column-gap: 1em;
  column-rule: thin dotted #999;
}
```

### Tipografía

En CSS, se pueden definir fuentes utilizando `@font-face` para importar fuentes personalizadas.

- **`@font-face`**: Permite definir y cargar una fuente personalizada.
  ```css
  @font-face {
    font-family: 'nombre_fuente';
    src: url('ruta_fuente');
    src: url('ruta_fuente-webfont.tipo1') format('tipo1'), ...;
  }

  .fuente {
    font-family: 'nombre_fuente';
  }
  ```

## Estilos en Listas

Las listas pueden ser estilizadas de diferentes maneras, tanto ordenadas como desordenadas:

### Selección de Listas y Elementos de Lista

- Se puede seleccionar la lista completa, cada elemento de la lista (`<li>`), e incluso agregar efectos a los elementos cuando se interactúa con ellos.

```css
#lista {
  list-style: none;
}

#lista li {
  display: inline; /* Muestra los elementos de la lista en línea */
}

#lista li:hover {
  color: blue; /* Cambia el color cuando el ratón está sobre un elemento */
}
```

### Propiedades de las Listas

- **`list-style-image`**: Permite usar una imagen personalizada como viñeta de la lista.
- **`list-style`**: Controla el tipo de viñeta (ninguna, círculo, cuadrado, etc.).

```css
ul {
  list-style-image: url('bullet.png'); /* Usa una imagen como viñeta */
  list-style: none; /* Elimina las viñetas */
}
```

## Modelo de Caja

El modelo de caja en CSS define cómo se calculan las dimensiones de un elemento. Cada elemento de la página se considera una "caja" que tiene las siguientes áreas:

- **Contenido**: El área donde se muestra el contenido del elemento.
- **Relleno (`padding`)**: Espacio entre el contenido y el borde.
- **Borde (`border`)**: Envoltura alrededor del relleno y el contenido.
- **Margen (`margin`)**: Espacio entre el borde del elemento y los elementos vecinos.

### Propiedades del Modelo de Caja

- **`width` y `height`**: Definen el ancho y alto del contenido del elemento.
  ```css
  div {
    width: 200px;
    height: 100px;
  }
  ```

- **`padding`**: Define el espacio entre el contenido y el borde del elemento. Puede especificarse para todos los lados o para cada lado por separado (top, right, bottom, left).
  ```css
  div {
    padding: 10px; /* Aplica 10px a todos los lados */
    padding: 10px 15px; /* Arriba/abajo 10px, izquierda/derecha 15px */
    padding: 10px 15px 20px 25px; /* top, right, bottom, left */
  }
  ```

- **`border`**: Define el borde del elemento. Puedes especificar el ancho, estilo y color del borde.
  ```css
  div {
    border: 2px solid black;
    border-radius: 5px; /* Bordes redondeados */
  }
  ```

- **`margin`**: Define el espacio entre el borde del elemento y los elementos adyacentes. También se puede especificar para cada lado.
  ```css
  div {
    margin: 20px auto; /* Arriba/abajo 20px, centrado a los lados */
  }
  ```

- **`box-sizing`**: Controla cómo se calculan el ancho y alto del elemento. Valores comunes:
  - `content-box` (por defecto): El `width` y `height` solo afectan al contenido.
  - `border-box`: El `width` y `height` incluyen el contenido, el padding y el borde.
  ```css
  div {
    box-sizing: border-box;
  }
  ```

---

## Maquetación con `<div>` y Estilos

La etiqueta `<div>` se utiliza para dividir la página web en secciones, permitiendo aplicar estilos específicos a cada una. Su comportamiento por defecto es ocupar todo el ancho disponible, lo cual permite una fácil maquetación del contenido.

### Propiedades de Posicionamiento
- **`position`**: Define cómo se posiciona el elemento en la página. Valores comunes:
  - `static` (por defecto): El elemento sigue el flujo normal del documento.
  - `relative`: Se posiciona en relación a su posición original, permitiendo mover el elemento con `top`, `left`, `right` y `bottom`.
  - `absolute`: Se posiciona en relación al contenedor más cercano con `position` distinto a `static`.
  - `fixed`: Se fija en la pantalla, sin moverse al hacer scroll.
  
  ```css
  div {
    position: absolute;
    top: 50px;
    left: 100px;
  }
  ```

- **Float y Clear**
  - **`float`**: Utilizado para colocar elementos a la izquierda o derecha de su contenedor, lo cual es útil para crear layouts.
    ```css
    .caja {
      float: left;
      width: 30%;
    }
    ```
  - **`clear`**: Se usa para controlar el comportamiento de elementos flotantes y evitar problemas de solapamiento.
    ```css
    .footer {
      clear: both;
    }
    ```

- **Centrado de Elementos**
  Para centrar cajas u otros elementos, es común envolverlos dentro de un `<div>` y aplicar márgenes automáticos:
  ```css
  .contenedor {
    width: 800px;
    margin: 0 auto; /* Arriba/abajo 0, Izquierda/derecha centrado */
  }
  ```

### Tipos de Diseño

- **Tamaños Fijos**: Define un ancho fijo (ej. 800px), útil para tener un diseño consistente.
- **Diseño Líquido**: Se adapta al tamaño de la ventana del navegador, utilizando `float` y `clear` para lograr un diseño flexible.

### Fondos

- **`background-image`**: Define una imagen de fondo para un elemento.
- **`background-position`**: Define la posición de la imagen de fondo (ej. `top`, `center`).
- **`background-repeat`**: Controla si la imagen se repite (ej. `repeat`, `no-repeat`).
- **`background-attachment`**: Define si la imagen de fondo se desplaza con el contenido (`scroll`) o se mantiene fija (`fixed`).

```css
div {
  background-image: url('fondo.png');
  background-position: center;
  background-repeat: no-repeat;
  background-attachment: fixed;
}
```

### Listas como Tablas
Las listas se pueden utilizar para estructurar contenido de manera similar a las tablas, especialmente con listas desordenadas (`<ul>`) y elementos de lista (`<li>`).

```css
#lista {
  list-style: none;
}

#lista li {
  display: inline; /* Muestra los elementos de la lista en línea */
}
```

## Formularios y Estilos

### Atributos y Agrupación de Formularios
- **`legend`**: Proporciona un título a un grupo de campos dentro de un formulario, mejorando la accesibilidad.
- **`fieldset`**: Agrupa los elementos de un formulario visualmente y lógicamente.
- **`label`**: Define etiquetas asociadas a los elementos del formulario para facilitar su uso.

```html
<fieldset>
  <legend>Información de Contacto</legend>
  <label for="nombre">Nombre:</label>
  <input type="text" id="nombre" name="nombre">
</fieldset>
```

### Propiedades Comunes en Formularios
- **`display: block`**: Hace que el elemento ocupe todo el ancho disponible.
- **`float`**: Alinea elementos a la izquierda o derecha.
- **`padding-right`**: Añade espacio a la derecha de un elemento.

- **Visibilidad**: Para controlar elementos visibles/invisibles en función de eventos, como `hover`.
  ```css
  #activador:hover #soyinvisible {
    visibility: visible;
    display: block; /* Muestra el elemento */
  }
  ```
### Validación con Pseudo-clases
- **Campos requeridos**: Utiliza `:required` para definir un campo que debe ser completado obligatoriamente.
  ```css
  input:required {
    border: 2px solid red;
  }
  ```
- **Campo con el foco**: Utiliza `:focus` para estilizar un campo cuando está seleccionado.
  ```css
  input:focus {
    background-color: lightyellow;
  }
  ```
- **Campo válido o inválido**: Utiliza `:valid` y `:invalid` para definir estilos dependiendo de si el campo cumple con los requisitos de validación.
  ```css
  input:valid {
    border: 2px solid green;
  }
  input:invalid {
    border: 2px solid red;
  }
  ```
## Contenedores Flexibles

Flexbox es una herramienta poderosa para crear layouts flexibles y alineados de manera consistente.

### Contenedor Flex
- **`display: flex`**: Define un contenedor flexible que permite que los elementos hijos se alineen de forma dinámica.
  ```css
  .contenedor-flex {
    display: flex;
    flex-direction: row; /* Fila horizontal */
    justify-content: space-between; /* Distribuye el espacio entre los hijos */
  }
  ```

- **`flex-direction`**: Define la dirección de los elementos hijos.
  - `row`: Los elementos se disponen en una fila.
  - `column`: Los elementos se disponen en una columna.

- **`justify-content`**: Alinea los elementos hijos a lo largo del eje principal.
  - `flex-start`: Alinea los elementos al inicio.
  - `flex-end`: Alinea los elementos al final.
  - `center`: Centra los elementos.
  - `space-between`: Espacio igual entre los elementos.
  - `space-around`: Espacio igual alrededor de los elementos.

- **`align-items`**: Alinea los elementos hijos a lo largo del eje transversal (vertical si `flex-direction` es `row`).
  - `stretch` (por defecto): Los elementos se estiran para llenar el contenedor.
  - `flex-start`, `flex-end`, `center`, `baseline`.

  ```css
  #container {
    display: flex;
    flex-direction: row;
    align-items: stretch;
  }
  ```

- **`flex-wrap`**: Controla si los elementos se envuelven o no cuando no caben en una línea.
  - `nowrap`: Todos los elementos se mantienen en una sola línea.
  - `wrap`: Los elementos se envuelven en nuevas líneas si es necesario.
  - `wrap-reverse`: Similar a `wrap`, pero con el orden invertido.

  ```css
  .contenedor-flex {
    display: flex;
    flex-wrap: wrap;
  }
  ```

- **`flex-grow`**: Define cómo crecerá un elemento en relación a los demás dentro del contenedor flex.
  ```css
  .flex-item {
    flex-grow: 2; /* Este elemento crecerá el doble que otros con flex-grow: 1 */
  }
  ```

- **`flex-shrink`**: Define cómo se reducirá un elemento si no hay suficiente espacio disponible.
  ```css
  .flex-item {
    flex-shrink: 1; /* Se reducirá normalmente */
  }
  ```

- **`flex-basis`**: Define el tamaño inicial del elemento antes de que se distribuya el espacio sobrante.
  ```css
  .flex-item {
    flex-basis: 100px;
  }
  ```

- **`order`**: Cambia el orden de los elementos en el contenedor flex.
  ```css
  .flex-item {
    order: 2; /* Los elementos con menor valor de `order` se colocan primero */
  }
  ```

- **Agrupación de Propiedades Flex**
  ```css
  .flex-item {
    flex: 1 0 100px; /* flex-grow, flex-shrink, flex-basis */
  }
  ```

## Variables CSS o Propiedades Personalizadas

Las variables CSS permiten definir valores reutilizables en tu hoja de estilos.

- **Definición**: Se definen con `--` y generalmente se colocan en `:root` para estar disponibles globalmente.
  ```css
  :root {
    --principal-color: #3498db;
    --padding-general: 10px;
  }
  ```

- **Uso**: Se utilizan con la función `var()`.
  ```css
  .boton {
    background-color: var(--principal-color);
    padding: var(--padding-general);
  }
  ```

## Efectos CSS3

### Sombras
- **Sombras de Texto (`text-shadow`)**: Añade sombras al texto.
  ```css
  h1 {
    text-shadow: 2px 3px 0px hsla(140, 3%, 36%, 0.5);
  }
  ```
- **Sombras de Caja (`box-shadow`)**: Añade sombras a las cajas.
  ```css
  div {
    box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.5);
  }
  ```

### Gradientes
- **Gradientes Lineales**
  ```css
  div {
    background: linear-gradient(90deg, #ccc 0%, #222 50%, #fff 100%);
  }
  ```
- **Gradientes Radiales**
  ```css
  div {
    background: radial-gradient(circle, orange 72%, red 100%);
  }
  ```
- **Repetición de Gradientes**
  ```css
  div {
    background: repeating-linear-gradient(90deg, #ccc 0px, hsla(0, 1%, 50%, 0.1) 5px);
  }
  ```

### Transiciones y Transformaciones

#### Transiciones
Las transiciones permiten aplicar varios estilos de manera gradual en función de una medida de tiempo.

- **Ejemplo básico de transición**
  ```css
  .clase:hover {
    transition: all 1s ease 0s;
    font-size: 26pt;
  }
  ```
- **Propiedades de Transición (Por separado)**
  - **`transition-property`**: Define las propiedades que cambiarán.
  - **`transition-duration`**: Especifica cuánto tiempo tomará la transición.
  - **`transition-timing-function`**: Define la velocidad de la transición (e.g., `ease`, `linear`, `ease-in`, `ease-out`, `ease-in-out`, `cubic-bezier`).
  - **`transition-delay`**: Define el tiempo de espera antes de que comience la transición.

- **Tipos de Animación**
  - **`linear`**: Velocidad uniforme durante la transición.
  - **`ease`**: Se acelera al inicio, luego se retarda y vuelve a acelerar al final.
  - **`ease-in`**: Aumenta progresivamente la velocidad.
  - **`ease-out`**: Desciende progresivamente la velocidad.
  - **`ease-in-out`**: Empieza y termina lentamente, con rapidez en la parte central.

#### Transformaciones
Las transformaciones permiten modificar la forma y posición de un elemento.

- **`scale()`**: Cambia el tamaño del elemento (valores positivos y negativos).
  ```css
  transform: scale(0.5);
  ```
- **`translate()`**: Cambia la posición del elemento.
  ```css
  transform: translate(10px, 20px);
  ```
- **`rotate()`**: Gira el elemento.
  ```css
  transform: rotate(25deg);
  ```
- **`skew()`**: Distorsiona el elemento a lo largo de los ejes X e Y.
  ```css
  transform: skew(5deg, 10deg);
  ```
- **`matrix()`**: Combinación de transformaciones que incluye traslación, escalado, rotación y sesgado.
  ```css
  transform: matrix(2.5, 0.1, 45, -10, 0, 0);
  ```
- **`transform-origin`**: Cambia el punto de origen de la transformación (ejes horizontal y vertical).
  ```css
  transform-origin: 10% 20%;
  ```

### Animaciones con Keyframes

- **Definición y Aplicación de Keyframes**
  ```css
  @keyframes movimiento {
    from {
      transform: translateX(0);
    }
    to {
      transform: translateX(100px);
    }
  }

  .caja {
    animation: movimiento 2.5s infinite ease-in;
  }
  ```
