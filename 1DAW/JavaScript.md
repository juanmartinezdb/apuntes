
- Funciones:  `function nombrefuncion (parametros){ instrucciones}`
# Mensajes
Ventanas que se lanzan desde el codigo al usuario.

- `alert(texto_del_mensaje)`  Avisa, solo se puede aceptar.
- `respuesta = prompt(texto_pregunta, valor_defecto)` Pide datos, el valor por defecto es opcional.
- `confirm(texto_mensaje)` se puede aceptar/rechazar (true/false)

# funciones predefinidas

- `eval("alert('Hola')")`  el texto se interpreta como si fuera codigo normal de JavaScript
- `parselInt(cadNumero,base) parseFloat(cadNumero)`  pasa un numero en string y lo castea  segun el segundo parametro que es opcional.
- `escape(texto) // unescape(texto)` muestra el ASCII del texto y viceversa.
- `isNaN(expresion)` true, si hay contenido **no** numerico.

## Metodos de String

- `anchor(nombre)`: Crea un marcador en el texto.
- `big()`: Muestra la cadena en fuente grande.
- `blink()`: Muestra el texto de modo intermitente.
- `bold()`: Muestra el texto en negrita.
- `charAt(n)`: Muestra el carácter en la posición `n`.
- `fixed()`: Muestra la cadena en fuente monoespaciada.
- `fontcolor(color)`: Establece el color del texto.
- `fontsize(n)`: Muestra el texto en tamaño `n` (1 a 7).
- `indexOf(cadenaInterna, inicio)`: Devuelve la posición de `cadenaInterna` desde `inicio`,(opcional). Deuvelve `-1` si no se encuentra.
-  `lastIndexOf(cadenaInterna, inicio)`: Devuelve la última posición de `cadenaInterna`.
- `italics()`: Muestra el texto en cursiva.
- `link(URL)`: Crea un hipervínculo con `URL`.
- `small()`: Muestra el texto en fuente pequeña.
- `strike()`: Texto tachado.
- `sub()`: Texto en subíndice.
- `substring(x, y)`: Muestra el texto desde la posición `x` hasta `y`.
- `sup()`: Texto en superíndice.
- `toLowerCase()`: Convierte el texto a minúsculas.
- `toUpperCase()`: Convierte el texto a mayúsculas.

- `length`: Almacena el tamaño de la cadena de texto.

## Métodos de `Math`

- `random()`: Genera un número aleatorio entre 0 y 1.-
- `abs(n)`: Valor absoluto de `n`.
- `max(x, y)`: El mayor entre `x` y `y`.
- `min(x, y)`: El menor entre `x` y `y`.
- `pow(x, y)`: Calcula 𝑥𝑦xy.
-  `sqrt(n)`: Raíz cuadrada de `n`.
- `ceil(n)`: Redondea `n` al entero más próximo hacia arriba.
- `floor(n)`: Redondea `n` al entero más próximo hacia abajo.
- `round(n)`: Redondea `n` al número entero más cercano.

- `tan(n)`: Tangente de `n`.
- `acos(n)`: Arco coseno de `n`.
- `asin(n)`: Arco seno de `n`.
- `atan(n)`: Arco tangente de `n`.
- `cos(n)`: Coseno de `n`.
- `sin(n)`: Seno de `n`.
- `exp(n)`: Calcula 𝑒𝑛en.
- `log(n)`: Logaritmo de `n`.

## Métodos del Objeto `Date()`

El objeto `Date()` representa fechas y horas. No permite trabajar con fechas anteriores a 1970 y cuenta los meses desde 0 (Enero) hasta 11 (Diciembre). 
`fecha = new Date();`

- `getDate()`: Día del mes.
- `getDay()`: Día de la semana como número.
- `getFullYear()`: Año en formato de cuatro dígitos.
- `getHours()`: Hora.
- `getMinutes()`: Minutos.
- `getMonth()`: Mes como número (0 a 11).
- `getSeconds()`: Segundos.
- `getTime()`: Milisegundos desde 1970.
- `getTimezoneOffset()`: Diferencia en minutos entre la zona horaria local y GMT.
- `setDate(valor)`: Establece el día del mes.
- `setFullYear(valor)`: Establece el año en cuatro dígitos.
- `setHours(valor)`: Establece la hora.
- `setMinutes(valor)`: Establece los minutos.
- `setMonth(valor)`: Establece el mes.
- `setSeconds(valor)`: Establece los segundos.
- `setTime(valor)`: Establece la fecha en milisegundos desde 1970.
- `toLocaleString()`: Devuelve la fecha según la zona horaria local

##  Arrays

- `nombreArray = new Array()`: Crea un array sin tamaño definido.
- `nombreArray[n] = valor`: Asigna un valor a la posición `n` del array.
- `nombreArray = new Array(tamaño)`: Crea un array con un tamaño predefinido.
- `equipos = new Array("Real Madrid", "F. C. Barcelona")`: Crea un array y asigna valores iniciales.
- `miOrdenador = new Array("HP", "Pentium III", 64)`: Un array puede contener diferentes tipos de datos.
- `elemento[3] = new Array(8)`: Crea un array y asigna otro array a una posición específica.

### Métodos de `Array`

- `concat(array)`: Combina dos arrays. Ejemplo: `c = a.concat(b)`.
- `join()`: Convierte los elementos del array en una cadena de texto. Ejemplo: `b = a.join()`.
- `reverse()`: Invierte el orden de los elementos del array.
- `sort()`: Ordena los elementos del array.
- `length`: Devuelve el número de elementos en el array.

# Objetos del Navegador

Son los objetos que el navegador pone a nuestra disposición para poder modificar los elementos de las páginas.

## `navigator` Representa la navegador

- `appCodeName`: Retorna 'Mozilla' para todos los navegadores.
- `appName`: Retorna el nombre del navegador, como 'Microsoft Internet Explorer' o 'Netscape'.
- `appVersion`: Muestra la versión completa del navegador.
- `language`/`browserLanguage`: Devuelve el idioma configurado en el navegador.
- `platform`: Información sobre el sistema operativo del usuario.
- `userAgent`: Detalles del navegador y sistema operativo del usuario.

## `screen`Propiedades de pantalla

- `width` y `height`: ancho y alto de la pantalla.
- `availWidth` y `availHeight`: ancho u alto disponible descontando la barra de tareas.
- `colorDepth`: Profundidad de color de la pantalla en bits por píxel.

## `window` ventana de la web.

si la pagina web tiene marcos, se generan tantos objetos windows como arcos.

- Boolean`closed`: Indica si una ventana ha sido cerrada.
- String `defaultStatus`: Mensaje por defecto de la barra de estado.
- windows [] `frames`: Array de los marcos de la ventana.
- `location`: Detalles de la URL actual.
- `name`: Nombre de la ventana.
- `parent`: Ventana padre de la actual, si es un marco sera la pagina con \<FRAMESET\>
- `self`: Referencia a la propia ventana.
- `top`: Referencia a la ventana superior.
- `status`: Mensaje actual de la barra de estado.

##### Métodos de `window`

- `   open(URL, nombreVentana, opcionesVentana)`: Abre una nueva ventana. Las opciones para la ventana se especifican como una cadena de texto, separadas por comas. Ejemplo de uso:    
    - `nuevaVentana = open("", "nueva", "toolbar=no,menubar=no,scrollbars=no,location=no,width=180,height=60")`.
        Opciones para el método `open`:
        - `toolbar`: Indica con "yes" o "no" si se muestra la barra de herramientas.
	    - `location`: Muestra o no la barra de dirección.
	    - `directories`: Muestra o no los botones de directorio.
	    - `status`: Permite mostrar u ocultar la barra de estado.
	    - `menubar`: Mostrar o no la barra de menús.
	    - `scrollbars`: Indica si se muestran las barras de desplazamiento.
	    - `resizable`: Permite ajustar el tamaño de la ventana.
	    - `width`: Ancho de la ventana en píxeles.
	    - `height`: Altura de la ventana en píxeles.
	    - `copyHistory`: Permite copiar el historial de páginas recorridas a la nueva ventana.
	    
- `close()`: Cierra la ventana.    
- `blur()`: Hace que la ventana deje de estar activa (pierde el foco).    
- `focus()`: Hace que la ventana sea la activa (tiene el "foco").
- `setInterval(expresiónjavascript, milisegundos)`: Ejecuta código JavaScript a intervalos regulares.
- `setTimeout(expresiónjavascript, milisegundos)`: Ejecuta código JavaScript después de un retraso.
- `clearTimeout(idTimeOut)`: Cancela un temporizador establecido con `setTimeout`.

### `location` 

Almacena información sobre la localización de la página de la venta lo cual permite cambiar dinámicamente la web.

- `href`: URL completa de la ventana.
- `hostname`: Nombre del host en la URL.
- `host`: Nombre del host con número de puerto.
- `pathname`: Ruta al recurso en la URL.
- `port`: Puerto utilizado en la URL.
- `hash`: Fragmento de la URL.
- `protocol`: Protocolo de la URL.
- `search`: Parte de la URL que sigue al signo de interrogación.

##### Métodos de `location`

- `replace(URL)`: Carga una nueva página y reemplaza la entrada actual en el historial.
- `reload()`: Recarga la página actual.

### `document` 
representa al contenido de una página web.

- `bgColor`: Color de fondo del documento.
- `fgColor`: Color del texto del documento.
- `linkColor`: Color de los enlaces no visitados.
- `vlinkColor`: Color de los enlaces visitados.
- `alinkColor`: Color de los enlaces activos.
- `images`: Array que contiene todas las imágenes del documento.
- `links`: Array que contiene todos los enlaces del documento.
- `lastModified`: Fecha de última modificación del documento.
- `URL`: URL del documento.
- `cookie`: Gestiona las cookies del documento.

##### Métodos de `document`

- `clear()`: Limpia el contenido del documento.
- `write(textoHTML)`: Escribe HTML en el documento.
- `writeln(textoHTML)`: Escribe HTML y añade un salto de línea.
- `close()`: Cierra el documento después de escribir.

### `history`
objeto que representa las direcciones de las paginas almacenas en el historial del navegador.
- `length`: Número de entradas en el historial del navegador.

##### Métodos de `history`

- `back()`: Navega a la página anterior en el historial.
- `forward()`: Navega a la página siguiente en el historial.
- `go(n)`: Navega a la página especificada en el historial. *-1 la anterior, -3 la antepenúltima*

## `image`
Objeto representa una imagen en el documento \<IMG\> y tiene sus mismas propiedades:

- `border`: Borde de la imagen.
- `height`: Altura de la imagen.
- `hspace`: Espacio horizontal alrededor de la imagen.
- `lowsrc`: URL de una imagen de baja resolución.
- `name`: Nombre de la imagen.
- `src`: URL de la imagen.
- `vspace`: Espacio vertical alrededor de la imagen.
- `width`: Ancho de la imagen.

## `link`
Representa cada enlace de la pagina creado con la etiqueta \<a\>

- `href`: URL del enlace.
- `hostname`: Nombre del host en la URL.
- `host`: Host y puerto en la URL.
- `pathname`: Ruta al recurso en la URL.
- `port`: Puerto utilizado en la URL.
- `hash`: Fragmento utilizado en la URL.
- `protocol`: Protocolo de la URL.
- `search`: Parte de la URL detrás del signo de interrogación.
- `target`: Destino del enlace en la ventana.

# FUNCIONES DE LOS EJERCICIOS

- `pintar = document.getElementById('resultado')` asigna la salida en la web, por ejemplo un div con la id Resultado
- `pintar.innerHTML = "La hora es" +ahora.getUTCHours() ` pasa la info a imprimir en el lugar asignado en la variable. 

- `document.getElementById('entrada1').innerHTML = "Primer valor → " + input1;`  declaramos donde va a salir y que va a salir del tirón. 

- `<body onload="funcion()">`  esa funcion se ejecuta al abrir la web directamente. 

- `document.write("<h2>El area del circulo es → " + area.toFixed(2) + "cm2</h2>");` escribe html en la web (donde esta el bloque de script).

- window.onclick = escucharEvento;

- window.onkeydown = escucharEvento;

- window.onmouseover = escucharEvento;

x.addEventListener('mouseover', mostrarSource);

x.addEventListener('mouseout', ocultarSource);
