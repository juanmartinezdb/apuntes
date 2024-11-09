# JavaScript Fundamentals: Events

## Índice
- Eventos
- Event Handlers (Manejadores de Eventos)
- `addEventListener` y `removeEventListener`
- Objeto `event`
- `preventDefault`
- Fases de Propagación: Burbujeo (Bubbling) y Captura (Capturing)
- `stopPropagation`
- Delegación de Eventos (Event Delegation)

## Eventos

- Un **evento** es una señal de que algo ha ocurrido.

### Tipos de Eventos

#### Eventos de Ratón (Mouse Events)
- **`click`**: Cuando se hace clic en un elemento (en dispositivos táctiles se genera al tocar).
- **`contextmenu`**: Cuando se hace clic derecho en un elemento.
- **`mouseover` / `mouseout`**: Cuando el cursor pasa por encima / deja un elemento.
- **`mousedown` / `mouseup`**: Cuando el botón del ratón es presionado / soltado sobre un elemento.
- **`mousemove`**: Cuando se mueve el ratón.

#### Eventos de Teclado (Keyboard Events)
- **`keydown`** y **`keyup`**: Cuando se presiona y suelta una tecla.

#### Eventos de Elementos de Formulario
- **`submit`**: Cuando el visitante envía un formulario (`<form>`).
- **`focus`**: Cuando el visitante enfoca un elemento, como un `<input>`.

#### Eventos del Documento
- **`DOMContentLoaded`**: Cuando el HTML está cargado y procesado, y el DOM está completamente construido.

#### Eventos CSS
- **`transitionend`**: Cuando una animación CSS termina.

- Existen muchos otros tipos de eventos en JavaScript.

## Manejadores de Eventos (Event Handlers)

- Los **manejadores de eventos** permiten detectar y reaccionar a los eventos que ocurren en una página web.
- Cada evento tiene un tipo (por ejemplo, "keydown", "focus", etc.) que lo identifica.
- La mayoría de los eventos se llaman en un elemento específico del DOM y luego se propagan a los ancestros de ese elemento, permitiendo que los manejadores asociados a esos elementos también puedan gestionarlos.
- Cuando se llama a un manejador de eventos, se le pasa un objeto `event` con información adicional sobre el evento.
  - Este objeto también tiene métodos que nos permiten detener la propagación (`stopPropagation`) y evitar el comportamiento predeterminado del navegador (`preventDefault`).

### Uso Anticuado del Manejador de Eventos

- No se recomienda usar manejadores directamente en el atributo HTML.
  ```html
  <button onClick="alert('¡Hola, manejador de eventos antiguo!');">Presióname</button>
  ```

### Manejador de Eventos usando Propiedad del DOM
- Se puede asignar un manejador de eventos usando una propiedad del DOM.
  ```html
  <input id="elem" type="button" value="Clickeame">
  <script>
    document.getElementById("elem").onclick = function () {
      alert('¡Gracias!');
    };
  </script>
  ```

## `addEventListener` y `removeEventListener`

### `addEventListener()`
- El método `addEventListener()` permite agregar un manejador de eventos a un elemento del DOM.
  ```html
  <input id="elem" type="button" value="Clickeame"/>
  <script>
    function handler1() {
      alert('¡Gracias!');
    }

    document.getElementById("elem").addEventListener("click", handler1); // ¡Gracias!
  </script>
  ```
- **Múltiples manejadores**: Llamar a `addEventListener()` varias veces permite agregar varios manejadores.
  ```html
  <input id="elem" type="button" value="Clickeame"/>
  <script>
    function handler1() {
      alert('¡Gracias!');
    }

    function handler2() {
      alert('¡Gracias de nuevo!');
    }

    document.getElementById("elem").addEventListener("click", handler1); // ¡Gracias!
    document.getElementById("elem").addEventListener("click", handler2); // ¡Gracias de nuevo!
  </script>
  ```

### `removeEventListener()`
- Para eliminar un manejador de eventos se utiliza `removeEventListener()`.
  ```javascript
  function handler() {
    alert('¡Gracias!');
  }

  input.addEventListener("click", handler);
  // ....
  input.removeEventListener("click", handler);
  ```

