# Guía de HTML5 - Apuntes y Glosario

Esta guía está organizada desde lo más básico hasta elementos más avanzados de HTML5. Sirve como referencia rápida para el trabajo diario, incluyendo las etiquetas principales, sus atributos y ejemplos prácticos.

## Índice
1. [Etiquetas básicas de estructura](#etiquetas%20b%C3%A1sicas%20de%20estructura)
2. [Etiquetas de texto](#etiquetas%20de%20texto)
3. [Enlaces e imágenes](#enlaces%20e%20im%C3%A1genes)
4. [Formularios y campos de formulario](#formularios%20y%20campos%20de%20formulario)
5. [Multimedia](#multimedia)
6. [Elementos semánticos](#elementos%20sem%C3%A1nticos)
7. [Etiquetas de contenido](#etiquetas%20de%20contenido)
8. [Etiquetas de formulario adicionales](#etiquetas%20de%20formulario%20adicionales)
9. [Tablas](#tablas)
10. [Contenido incrustado](#contenido%20incrustado)

---

## Etiquetas básicas de estructura

### `<html>`
Define el documento como HTML.
```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8">
    <title>Título del documento</title>
  </head>
  <body>
    <p>Contenido aquí.</p>
  </body>
</html>
```

### `<head>`
Contiene metadatos sobre el documento: títulos, enlaces a CSS, scripts, etc.

- **`<meta>`**: Define metadatos, como la codificación de caracteres (`charset="UTF-8"`) y descripción (`name="description" content="Ejemplo"`).
- **`<title>`**: Define el título del documento.
- **`<link>`**: Enlace a documentos externos, como hojas de estilo CSS.
```html
<link rel="stylesheet" href="formato.css" >
```
- **`<style>`**: Define CSS interno.
- **`<script>`**: Código JavaScript, también puede colocarse al final del `<body>`.

### `<body>`
Contiene todo el contenido visible del documento.
```html
<body>
  <h1>Hola, mundo</h1>
  <p>Este es el contenido principal del sitio web.</p>
</body>
```

### Comentarios
Los comentarios se añaden con `<!-- -->` y no se muestran en la página.
```html
<!-- Este es un comentario -->
```

### Etiquetas auto-cerradas
Algunas etiquetas no necesitan etiqueta de cierre:
- **`<br>`**: Salto de línea.
- **`<hr>`**: Línea horizontal.
- **`<img>`**: Imagen.
- **`<input>`**: Campo de entrada de datos.
- **`<meta>`**: Metadatos del documento.
- **`<link>`**: Enlace a recursos externos.
- **`<wbr>`**: Salto de línea sugerido.

---

## Etiquetas de texto

### `<h1>` - `<h6>`
Etiquetas de encabezado, `<h1>` es el título más importante y `<h6>` el menos.
```html
<h1>Encabezado principal</h1>
<h2>Sub-encabezado</h2>
```

### `<p>`
Define un párrafo.
```html
<p>Este es un párrafo de ejemplo.</p>
```

### `<strong>` y `<em>`
**`<strong>`**: Da énfasis fuerte (negrita).
**`<em>`**: Da énfasis sutil (cursiva).
```html
<p>Este es un <strong>texto importante</strong> y un <em>texto enfatizado</em>.</p>
```

### `<ul>`, `<ol>`, `<li>`
**`<ul>`**: Lista desordenada. 
**`<ol>`**: Lista ordenada. 
**`<li>`**: Elemento de lista.
```html
<ul>
  <li>Elemento uno</li>
  <li>Elemento dos</li>
</ul>

<ol>
  <li>Primero</li>
  <li>Segundo</li>
</ol>
```

### `<blockquote>` y `<q>`
**`<blockquote>`**: Contenido citado desde otra fuente. Puede incluir el atributo `cite` para especificar la fuente.
**`<q>`**: Cita breve en línea, se muestra entre comillas.
```html
<blockquote cite="https://example.com">
  Esta es una cita de una fuente externa.
</blockquote>
<p>Según el autor: <q>Este es un fragmento citado</q>.</p>
```

### `<pre>`
Muestra texto con espacios y saltos de línea tal y como se escriben.
```html
<pre>
  Texto con formato
  conservado.
</pre>
```

### `<mark>`, `<small>`, `<s>` y `<u>`
**`<mark>`**: Resalta el texto.
**`<small>`**: Texto de menor importancia.
**`<s>`**: Texto tachado.
**`<u>`**: Texto subrayado.
```html
<p>Este es un <mark>texto resaltado</mark>, un <small>comentario pequeño</small>, un <s>texto tachado</s> y un <u>texto subrayado</u>.</p>
```

### `<abbr>` y `<dfn>`
**`<abbr>`**: Define una abreviatura y muestra un tooltip al pasar el cursor (atributo `title`).
**`<dfn>`**: Marca un término definido.
```html
<p><abbr title="Hypertext Markup Language">HTML</abbr> es un lenguaje de marcado.</p>
<p>El término <dfn>API</dfn> significa Application Programming Interface.</p>
```

### `<code>`, `<var>`, `<sub>`, `<sup>`
**`<code>`**: Muestra código fuente.
**`<var>`**: Define una variable.
**`<sub>`** y **`<sup>`**: Subíndice y superíndice, respectivamente.
```html
<p>El código es: <code>console.log("Hola")</code></p>
<p>Variable: <var>x</var></p>
<p>H<sub>2</sub>O y E=mc<sup>2</sup></p>
```

---

## Enlaces e imágenes

### `<a>`
Define un enlace. 
**Atributos**:
- `href`: Dirección a la que apunta el enlace.
- `target`: Define si el enlace se abre en una nueva pestaña (`_blank`).
- `download`: Permite descargar el archivo enlazado.
```html
<a href="https://example.com" target="_blank" download="archivo.pdf">Descargar archivo</a>
```

### `<img>`
Inserta una imagen. 
**Atributos**:
- `src`: Fuente de la imagen.
- `alt`: Texto alternativo para accesibilidad.
- `title`: Texto descriptivo al pasar el cursor.
```html
<img src="imagen.jpg" alt="Descripción de la imagen" title="Imagen de ejemplo">
```

---

## Formularios y campos de formulario

### `<form>`
Define un formulario HTML.
**Atributos**:
- `action`: URL a la que se envían los datos del formulario.
- `method`: Método de envío (`GET` o `POST`).
```html
<form action="/enviar" method="post">
  <label for="nombre">Nombre:</label>
  <input type="text" id="nombre" name="nombre">
  <button type="submit">Enviar</button>
</form>
```

### `<input>`
Campo de entrada de datos.
**Atributos comunes**:
- `type`: Define el tipo de entrada (`text`, `password`, `email`, etc.).
- `name`: Nombre del campo.
- `placeholder`: Texto de sugerencia.
- `required`: Campo obligatorio.
- `readonly`: Campo de solo lectura.
- `disabled`: Campo deshabilitado.
```html
<input type="email" name="correo" placeholder="Introduce tu correo" required>
```

### `<select>` y `<option>`
Define una lista desplegable.
- **`<option>`**: Define una opción de la lista.
- **`<optgroup>`**: Agrupa varias opciones relacionadas.
```html
<label for="frutas">Elige una fruta:</label>
<select id="frutas" name="frutas">
  <optgroup label="Frutas dulces">
    <option value="manzana">Manzana</option>
    <option value="banana">Banana</option>
  </optgroup>
  <optgroup label="Frutas cítricas">
    <option value="naranja">Naranja</option>
    <option value="limón">Limón</option>
  </optgroup>
</select>
```

### `<textarea>`
Área de texto de varias líneas.
**Atributos**:
- `rows`: Número de líneas visibles.
- `cols`: Ancho del área de texto.
```html
<textarea id="comentarios" name="comentarios" rows="4" cols="50">Escribe aquí tus comentarios...</textarea>
```

### `<fieldset>` y `<legend>`
**`<fieldset>`**: Agrupa campos relacionados en un formulario.
**`<legend>`**: Define un título para el grupo.
```html
<fieldset>
  <legend>Información personal</legend>
  <label for="nombre">Nombre:</label>
  <input type="text" id="nombre" name="nombre">
  <label for="edad">Edad:</label>
  <input type="number" id="edad" name="edad">
</fieldset>
```

---

## Multimedia

### `<audio>`
Define contenido de audio.
**Atributos**:
- `controls`: Muestra controles de reproducción.
```html
<audio controls>
  <source src="audio.mp3" type="audio/mpeg">
  Tu navegador no soporta la reproducción de audio.
</audio>
```

### `<video>`
Define contenido de video.
**Atributos**:
- `controls`: Muestra controles de reproducción.
- `width` y `height`: Dimensiones del video.
```html
<video width="640" height="360" controls>
  <source src="video.mp4" type="video/mp4">
  Tu navegador no soporta la reproducción de video.
</video>
```

### `<figure>` y `<figcaption>`
**`<figure>`**: Contenido visual como imágenes, diagramas, multimedia.
**`<figcaption>`**: Leyenda para `<figure>`.
```html
<figure>
  <img src="diagrama.png" alt="Diagrama de flujo">
  <figcaption>Figura 1: Diagrama de flujo</figcaption>
</figure>
```

---

## Elementos semánticos

### `<header>`
Define un encabezado para un documento o sección.
```html
<header>
  <h1>Bienvenido a mi sitio web</h1>
  <nav>
    <a href="#">Inicio</a>
    <a href="#">Contacto</a>
  </nav>
</header>
```

### `<footer>`
Define un pie de página.
```html
<footer>
  <p>Derechos reservados &copy; 2024</p>
</footer>
```

### `<section>` y `<article>`
**`<section>`**: Agrupa contenido relacionado.
**`<article>`**: Define un contenido independiente, como un artículo de blog.
```html
<section>
  <h2>Sección de noticias</h2>
  <article>
    <h3>Noticia 1</h3>
    <p>Contenido de la noticia...</p>
  </article>
</section>
```

### `<nav>`
Define un menú de navegación.
```html
<nav>
  <a href="#">Inicio</a>
  <a href="#">Servicios</a>
  <a href="#">Contacto</a>
</nav>
```

### `<aside>`
Contenido relacionado lateralmente, como enlaces a otros artículos o anuncios.
```html
<aside>
  <h4>Enlaces relacionados</h4>
  <ul>
    <li><a href="#">Artículo relacionado 1</a></li>
    <li><a href="#">Artículo relacionado 2</a></li>
  </ul>
</aside>
```

### `<main>`
Contenido principal del documento, debe usarse una sola vez.
```html
<main>
  <h2>Contenido principal</h2>
  <p>Este es el contenido más relevante de la página.</p>
</main>
```

### `<address>`
Define información de contacto.
```html
<address>
  Puedes contactarnos en: <a href="mailto:info@example.com">info@example.com</a>
</address>
```

### `<time>`
Define una fecha u hora específica.
```html
<p>Publicado el <time datetime="2024-11-09">9 de noviembre de 2024</time>.</p>
```

---

## Etiquetas de contenido

### `<hr>`
Cambio temático entre párrafos, se muestra como una línea horizontal.
```html
<p>Este es un párrafo.</p>
<hr>
<p>Este es otro párrafo después de un cambio temático.</p>
```

### `<div>`
Contenedor genérico sin ningún significado especial. Utilizado para aplicar estilos con CSS o manipular elementos con JavaScript.
```html
<div class="contenedor">
  <p>Contenido dentro del div.</p>
</div>
```

---

## Etiquetas de formulario adicionales

### `<button>`
Botón que permite enviar contenido HTML adicional.
**Atributos**:
- `type`: Define el tipo de botón (`submit`, `reset`, `button`).
```html
<button type="submit">Enviar</button>
<button type="reset">Restablecer</button>
```

### `<label>`
Asocia un campo de formulario con una etiqueta descriptiva.
**Atributo**:
- `for`: Identificador del campo al que hace referencia.
```html
<label for="email">Correo electrónico:</label>
<input type="email" id="email" name="email">
```

### `<datalist>`
Proporciona una lista de opciones sugeridas para un campo `<input>`.
```html
<label for="navegador">Elige un navegador:</label>
<input list="navegadores" id="navegador" name="navegador">
<datalist id="navegadores">
  <option value="Chrome">
  <option value="Firefox">
  <option value="Safari">
  <option value="Edge">
</datalist>
```

---

## Tablas

### `<table>`
Define una tabla.
- **`<tr>`**: Fila de la tabla.
- **`<th>`**: Celda de encabezado.
- **`<td>`**: Celda de datos.
```html
<table>
  <caption>Ejemplo de tabla</caption>
  <tr>
    <th>Encabezado 1</th>
    <th>Encabezado 2</th>
  </tr>
  <tr>
    <td>Celda 1</td>
    <td>Celda 2</td>
  </tr>
</table>
```

---

## Contenido incrustado

### `<iframe>`
Representa un contexto anidado de navegación.
```html
<iframe src="https://www.example.com" width="600" height="400"></iframe>
```

### `<embed>` y `<object>`
Permite incrustar contenido externo.
- **`<embed>`**: Generalmente utilizado para contenido multimedia.
- **`<object>`**: Recurso externo que puede ser tratado como una imagen, documento HTML, etc.
```html
<object data="documento.pdf" type="application/pdf" width="600" height="400"></object>
```

### `<canvas>` y `<svg>`
- **`<canvas>`**: Área para gráficos con JavaScript.
- **`<svg>`**: Gráficos vectoriales embebidos.
```html
<canvas id="miCanvas" width="500" height="500"></canvas>
<svg width="100" height="100">
  <circle cx="50" cy="50" r="40" stroke="black" stroke-width="3" fill="red" />
</svg>
```

Espero que estos apuntes complementados te sigan siendo útiles y prácticos. ¡Dime si necesitas ampliar o ajustar algo más!
