# JavaScript Fundamentals: Date

## Objeto Date

- El objeto **Date** en JavaScript se utiliza para trabajar con fechas y horas.
- Permite crear fechas, obtener valores individuales de la fecha (como el año, mes, día), y manipularlos.

### `Date.parse()`
- Transforma una cadena con la representación de una fecha y hora, y devuelve el número de milisegundos desde las 00:00:00 del 1 de enero de 1970, hora local.
  ```javascript
  const d = Date.parse("March 21, 2012");
  console.log(d); // Milisegundos desde el 1 de enero de 1970
  ```

### Métodos Importantes de Date

#### Métodos `set` y `get`
- Son métodos que permiten cambiar el valor de alguna parte de la fecha (`set`) o de obtener el valor de alguna parte de la fecha (`get`).

- Ejemplos:
  - **`setMonth(mes)`** y **`getMonth()`**: Cambia y obtiene el mes (0-11).
    ```javascript
    let fecha = new Date();
    fecha.setMonth(5); // Establece junio (los meses son indexados desde 0)
    console.log(fecha.getMonth()); // 5
    ```

  - **`setDate(día)`** y **`getDate()`**: Cambia y obtiene el día del mes (1-31).
    ```javascript
    fecha.setDate(15);
    console.log(fecha.getDate()); // 15
    ```

  - **`setHours(hora, minuto, segundo)`** y **`getHours()`**: Cambia y obtiene la hora (0-23).
    ```javascript
    fecha.setHours(10, 30, 0); // Establece las 10:30:00
    console.log(fecha.getHours()); // 10
    ```

#### `getDay()`
- Devuelve el día de la semana, numerados del 0 (domingo) al 6 (sábado).
  ```javascript
  let diaSemana = fecha.getDay();
  console.log(diaSemana); // 0 para domingo, 1 para lunes, etc.
  ```

#### `toDateString()`
- Convierte la fecha del objeto a una cadena con formato legible.
  ```javascript
  console.log(fecha.toDateString()); // Ejemplo: "Tue Jun 15 2022"
  ```

#### `toGMTString()` y `toUTCString()`
- **`toGMTString()`**: Convierte la fecha del objeto a una cadena con formato de fecha GMT.
  ```javascript
  console.log(fecha.toGMTString()); // Ejemplo: "15 Jun 2022 08:00:00 GMT"
  ```
- **`toUTCString()`**: Convierte la fecha del objeto a una cadena con formato de fecha UTC.
  ```javascript
  console.log(fecha.toUTCString()); // Ejemplo: "15 Jun 2022 08:00:00 GMT"
  ```

### Ejemplo de Uso de Date

- Crear una nueva instancia de `Date` y modificar la fecha.
  ```javascript
  let d = new Date(); // Establece una variable tipo fecha/hora con la del tiempo de ejecución

  d.setDate(d.getDate() + 7); // Añade una semana a la fecha actual
  console.log(d.toDateString()); // Muestra la nueva fecha
  