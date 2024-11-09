# Índice
1. [CSS Grid](#css%20grid)
2. [Centrando Elementos](#centrando%20elementos)
3. [Scroll Snap](#scroll%20snap)
4. [Scroll Behavior](#scroll%20behavior)
5. [Cursores](#cursores)
6. [Media Queries](#media%20queries)
7. [Efecto Parallax](#efecto%20parallax)
8. [Menú Horizontal](#menú%20horizontal)
9. [Propiedad Overflow](#propiedad%20overflow)
10. [Iconos](#iconos)
11. [Botones CSS](#botones%20css)
12. [Migas de Pan (Breadcrumb)](#migas%20de%20pan%20breadcrumb)
13. [Tooltip](#tooltip)
14. [Modo Oscuro y Claro](#modo%20oscuro%20y%20claro)
15. [Acortar Texto](#acortar%20texto)
16. [Efectos Visuales con CSS](#efectos%20visuales%20con%20css)
17. [Mezclar Imágenes con Color (Blend Modes)](#mezclar%20imágenes%20con%20color%20blend%20modes)

# CSS Grid
[Back](#Índice)
- **CSS Grid** permite maquetar contenido ajustándolo a rejillas configurables en CSS. Es bidimensional, a diferencia de Flexbox.
- En el contenedor se usa la propiedad `display` con valor `inline-grid` (en línea con el contenido) o `grid` (en bloque).

### Propiedades de CSS Grid
- **`grid-template-columns`**: Tamaño de columnas.
  ```css
  grid-template-columns: repeat(3, 1fr);
  ```
- **`grid-template-rows`**: Tamaño de las filas (puede ser `auto`, en `px`, `%`, `fr`, etc.).
- **`row-gap`**: Espaciado entre filas.
- **`column-gap`**: Espaciado entre columnas.
- **`grid-gap`**: Espaciado para filas y columnas (primer valor para filas, segundo para columnas).

```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 10px 20px;
}
```

# Centrando Elementos
[Back](#Índice)
### Métodos para Centrar Horizontal y Verticalmente

- **Con Flexbox** (funciona para todos los elementos)
  ```css
  justify-content: center;
  align-items: center;
  ```
- **Solo para textos**
  ```css
  text-align: center;
  line-height: 200px;
  ```
- **Para Imágenes** (utilizando posición absoluta y la propiedad transform)
  ```css
div img {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  -webkit-transform: translate(-50%, -50%);
}
```
- **Elemento dentro de un Grid**
  ```css
  display: grid;
  place-items: center;
  ```
- **Texto al lado de imagen/input**
  ```css
  img {
    vertical-align: middle;
  }
  ```
- **Centrado Absoluto para Elementos**
  ```css
  .clase {
    position: absolute;
    top: 50%;
    left: 50%;
    margin-top: -50px; /* Ajusta el valor según la mitad de la altura del elemento */
    margin-left: -50px; /* Ajusta el valor según la mitad del ancho del elemento */
  }
  ```
- **Alinear verticalmente texto dentro de un div**
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
- **Usar el tamaño de la página con viewport**
  ```css
  height: 100vh;
  ```

# Scroll Snap
[Back](#Índice)
Permite crear desplazamiento o scroll en contenedores para una navegación fluida y organizada entre secciones de contenido.

### Propiedades de Scroll Snap

```css
.contenedor-scroll {
  scroll-snap-type: [x | y | block | inline] [mandatory | proximity];
}

.seccion {
  scroll-snap-align: [start | center | end | none]; /* Alineación de los elementos hijos */
}
```

- **`scroll-snap-type`**:
  - `x`: Eje horizontal.
  - `y`: Eje vertical.
  - `block`: En bloque.
  - `inline`: En líneas.
  - `mandatory`: Se detiene en los anclajes.
  - `proximity`: Punto más cercano.

# Scroll Behavior
[Back](#Índice)
Permite realizar transiciones suaves y animadas entre marcadores.

- **Propiedad `scroll-behavior` en HTML**
  ```css
  html {
    scroll-behavior: auto | smooth;
  }
  ```

# Cursores
[Back](#Índice)
Permite cambiar el aspecto del puntero del ratón usando la propiedad `cursor`.

- **Propiedad `cursor`**
  ```css
  cursor: pointer;
  ```
- **Tipos Comunes**: `crosshair`, `help`, `move`, `pointer`, `progress`, `text`, `wait`, `zoom-in`, `alias`, `grab`, `not-allowed`, etc.

# Media Queries
[Back](#Índice)
### Uso de Media Queries para Diseño Responsivo

Los media queries permiten variar los estilos según las condiciones del dispositivo. Ejemplo para pantallas de un ancho máximo de 800px:

```css
@media (max-width: 800px) {
  .sidebar {
    display: none;
  }
}
```

- **Tipos de medios**: `all`, `print`, `screen`, `speech`.
- **Operadores lógicos**: `AND`, `OR`, `NOT`.
  ```css
  @media (max-width: 800px), tty and (orientation: portrait) {}
  @media not screen and (color) {}
  ```
- **Ancho mínimo y máximo**
  ```css
  @media (min-width: 768px) {}
  @media (max-width: 767px) {}
  ```

### Mobile First y Desktop First

- **Mobile First**: Se diseña primero para móviles y luego se aplican ajustes con media queries para tabletas y escritorios.
  ```css
  @media (min-width: 600px) { /* Para tabletas */ }
  @media (min-width: 1024px) { /* Para escritorio */ }
  ```

- **Desktop First**: Ajustes para dispositivos más pequeños después del diseño de escritorio.
  ```css
  @media (min-width: 600px) and (max-width: 1023px) { /* Para tabletas */ }
  @media (max-width: 599px) { /* Para móviles */ }
  ```

### Problemas Comunes
- **Conflictos de Estilos**: Puede haber conflictos si varias media queries coinciden.
- **Prioridad**: La última media query definida tiene prioridad.

# Efecto Parallax
[Back](#Índice)
Crea una sensación de profundidad haciendo que el contenido de la página se mueva a diferentes velocidades.

### Implementación Básica

- **Estructura HTML**
  ```html
  <div class="contenedor">
    <div class="contenido">
      <p>Contenido</p>
    </div>
  </div>
  ```

- **Propiedades del contenedor**
  ```css
  .contenedor {
    background-image: url('fondo.jpg');
    background-size: cover;
    background-attachment: fixed;
    height: 500px;
    background-position: center;
    background-repeat: no-repeat;
  }
  ```

# Menú Horizontal
[Back](#Índice)
Un menú horizontal se crea usando una lista desordenada cuyos elementos (`<li>`) son ítems del menú.

### Estructura HTML Básica

```html
<header>
  <nav>
    <ul>
      <li><a href="#">Inicio</a></li>
      <li><a href="#">Contacto</a></li>
    </ul>
  </nav>
</header>
```

### Estilos CSS NAV SUBMENUS

```css
nav ul {
  list-style: none;
}
nav li {
  display: inline;
}
```

- **Submenú Desplegable**
  ```css
  #submenu {
    visibility: hidden;
  }

  li:hover ul#submenu {
    visibility: visible;
  }

  #submenu li {
    float: none; /* Debajo del li asociado */
  }
  ```
  - **Ejemplo**  
```css
nav ul {
    list-style: none;
    padding: 0;
    margin: 0;
}
nav li {
    display: inline;
    margin-right: 20px;
}
nav a {
    text-decoration: none;
    color: black;
    font-weight: bold;
}

/* Submenú desplegable */
#submenu {
    visibility: hidden;
    list-style: none;
    padding: 0;
    position: absolute;
    background-color: #f9f9f9;
    margin-top: 10px;
}
li:hover ul#submenu {
    visibility: visible;
}
#submenu li {
    float: none;
}

/* Menú con Flexbox */
header {
    display: flex;
    justify-content: space-between;
    flex-direction: column;
    padding: 20px;
    background-color: #ddd;
}
nav ul li {
    flex-grow: 1;
}

```

```html
  <nav>
            <ul>
                <li><a href="#">Inicio</a></li>
                <li><a href="#">Servicios</a>
                    <!-- Submenú desplegable -->
                    <ul id="submenu">
                        <li><a href="#">Servicio 1</a></li>
                        <li><a href="#">Servicio 2</a></li>
                        <li><a href="#">Servicio 3</a></li>
                    </ul>
                </li>
                <li><a href="#">Contacto</a></li>
            </ul>
        </nav>
```

- **Menú con Flexbox**
  ```css
  header {
    display: flex;
    justify-content: space-between;
    flex-direction: column;
  }
  nav ul li {
    flex-grow: 1;
  }
  ```


# Propiedad Overflow
[Back](#Índice)
Controla el comportamiento del contenido que se encuentra en una caja o contenedor.

- **Valores de `overflow`**
  - `visible`: El contenido se desborda y es visible (valor por defecto).
  - `hidden`: El contenido que se desborda se oculta.
  - `scroll`: Se muestran barras de desplazamiento.
  - `auto`: El navegador decide si muestra barras de desplazamiento.

- **Overflow Horizontal y Vertical**
  ```css
  overflow-x: hidden;
  overflow-y: scroll;
  ```

# Iconos
[Back](#Índice)
### Iconos de Google

- **Incluir la hoja de estilos en el `<head>`**
  ```html
  <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
  ```
- **Insertar un icono con i o span**
  ```html
  <span class="material-icons">favorite</span>
  ```
- **Personalización**: Se puede cambiar el tamaño, color, efectos, etc. desde CSS.

# Botones CSS
[Back](#Índice)
### Botones con Efectos

- **Botón con Degradado**
  ```css
  .boton {
    background-image: linear-gradient(to right, #ff7e5f, #feb47b);
  }
  ```
- **Efecto de Pulsación**
  ```css
  .pulsar {
    transition: transform 0.3s ease-in-out;
  }
  .pulsar:active {
    transform: scale(0.9);
  }
  ```
- **Botones con Iconos (Font Awesome)**
  ```html
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
  <button class="boton1"><i class="fas fa-exclamation-circle"></i> Primary</button>
  <button class="boton2"><i class="fas fa-exclamation-triangle"></i> Warning</button>
  ```

# Migas de Pan (Breadcrumb)
[Back](#Índice)
### Estructura HTML

```html
<ul class="migas">
  <li><a href="#">Home</a></li>
  <li><a href="#">Contact</a></li>
</ul>
```

### Estilos CSS

```css
ul.migas {
  list-style: none;
}

ul.migas li {
  display: inline;
}

ul.migas li + li:before {
  content: "/\00a0"; /* Separador */
}
```

# Tooltip
[Back](#Índice)
### Implementación Básica

- **Estructura HTML**
  ```html
  <div class="caja">
    <span class="mje">Mensaje del tooltip</span>
    Mi elemento
  </div>
  ```

- **Estilos CSS**
  ```css
  .caja {
    position: relative;
    display: inline-block;
  }

  .mje {
    visibility: hidden;
  }

  .caja:hover .mje {
    visibility: visible;
    opacity: 1;
  }
  ```

# Modo Oscuro y Claro
[Back](#Índice)
### `prefers-color-scheme`

Característica de las media queries que detecta si el usuario tiene una preferencia de esquema de color.

```css
@media (prefers-color-scheme: dark) {
  body {
    background-color: black;
    color: white;
  }
}
```

# Acortar Texto
[Back](#Índice)
Para limitar el número de líneas y mostrar puntos suspensivos (`...`) se utiliza la propiedad `line-clamp` junto con otras propiedades.

### Propiedades para Acortar Texto

```css
.acortar {
  display: -webkit-box;
  -webkit-line-clamp: 3; /* Número de líneas */
  -webkit-box-orient: vertical;
  overflow: hidden;
}
```

- **`hyphens`**: Controla la división de palabras al final de una línea.
  - `auto`: El navegador decide dónde dividir.
  - `manual`: Utiliza el carácter de guion (`-`) para dividir.
  - `none`: Desactiva la división automática y manual de palabras.

# Efectos Visuales con CSS
[Back](#Índice)
La propiedad `filter` de CSS permite aplicar efectos visuales a los elementos de la página.

### Sintaxis General
```css
filter: <función-de-filtro>(<valor>);
```

### Funciones de Filtro y Descripción

| Función                | Descripción                                | Valores                             |
|------------------------|--------------------------------------------|-------------------------------------|
| `blur(<valor>)`        | Aplica un desenfoque al elemento           | `<valor>`: cantidad de desenfoque a aplicar |
| `brightness(<valor>)`  | Ajusta el brillo del elemento              | `0`: completamente oscuro, `1`: original     |
| `contrast(<valor>)`    | Ajusta el contraste del elemento           | `0`: completamente gris, `1`: original       |
| `grayscale(<valor>)`   | Convierte el elemento a escala de grises   | `0`: original, `1`: escala de grises         |
| `hue-rotate(<valor>)`  | Gira el espectro de colores del elemento   | `<valor>`: grados de 0 a 360deg              |
| `invert(<valor>)`      | Invierte los colores del elemento          | `0`: original, `1`: invertido                |
| `opacity(<valor>)`     | Ajusta la opacidad del elemento            | `0`: transparente, `1`: original             |
| `saturate(<valor>)`    | Ajusta la saturación del elemento          | `0`: grisáceo, `100%`: original              |
| `sepia(<valor>)`       | Aplica un tono sepia al elemento           | `0`: original, `1`: sepia completo           |

---

# Mezclar Imágenes con Color (Blend Modes)
[Back](#Índice)
`Blend Modes` permite combinar elementos HTML con otros elementos de fondo.

### Sintaxis General
```css
mix-blend-mode: <efecto>;
```

### Tipos de Blend Modes

| Blend Mode       | Descripción                                                        | Características                               |
|------------------|--------------------------------------------------------------------|-----------------------------------------------|
| `multiply`       | Multiplica los colores de la capa superior con los de la capa inferior | Oscurece la imagen resultante                  |
| `screen`         | Invierte los colores de la capa superior y los multiplica con los de la capa inferior | Aclara las áreas de la imagen                  |
| `overlay`        | Combina `multiply` y `screen`, oscureciendo o aclarando según los colores | Produce un efecto de contraste y saturación    |
| `darken`         | Conserva los colores más oscuros de las dos capas                   | Selecciona el color más oscuro de cada píxel   |
| `lighten`        | Conserva los colores más claros de las dos capas                    | Selecciona el color más claro de cada píxel    |
| `color-dodge`    | Aclara los colores de la capa inferior dependiendo de los colores de la capa superior | Aclara las áreas de la imagen                  |
| `color-burn`     | Oscurece los colores de la capa inferior dependiendo de los colores de la capa superior | Oscurece las áreas de la imagen                |
| `difference`     | Resta los colores de la capa superior de los de la capa inferior    | Produce un efecto de inversión de colores      |

---

Si necesitas más ejemplos prácticos de cómo implementar estos efectos o deseas aclaraciones adicionales, házmelo saber. ¡Estoy aquí para ayudarte!
