# JavaScript Fundamentals: Strings

## Strings son Inmutables

- Los **strings** en JavaScript son **inmutables**, lo que significa que no se pueden cambiar una vez creados.
- Los tipos primitivos, excepto `null` y `undefined`, proporcionan muchos métodos útiles.
- Formalmente, estos métodos funcionan a través de objetos temporales.
  ```javascript
  let str = 'Hi';
  console.log(str[0]); // H

  str[0] = 'h'; // Error: no se puede cambiar directamente
  console.log(str[0]); // No funciona
  ```

- La solución usual para cambiar un string es crear un nuevo string completo y asignarlo a la variable original.
  ```javascript
  let str = 'Hi';
  str = 'h' + str[1]; // reemplaza el string
  console.log(str); // hi
  ```

## Métodos de String

### Métodos Comunes
- **`charAt()`**: Devuelve el carácter en un índice específico.
  ```javascript
  let str = "Hola";
  console.log(str.charAt(1)); // o
  ```

- **`charCodeAt()`**: Devuelve el valor Unicode del carácter en un índice específico.
  ```javascript
  console.log(str.charCodeAt(1)); // 111 (Unicode de 'o')
  ```

- **`concat()`**: Une dos o más strings y devuelve el resultado.
  ```javascript
  let saludo = "Hola";
  let mundo = " Mundo";
  console.log(saludo.concat(mundo)); // Hola Mundo
  ```

- **`endsWith()`**: Devuelve `true` si el string termina con un valor especificado.
  ```javascript
  console.log(saludo.endsWith("a")); // true
  ```

- **`includes()`**: Devuelve `true` si el string contiene un valor especificado.
  ```javascript
  console.log(saludo.includes("la")); // true
  ```

- **`indexOf()`**: Devuelve el índice de la primera ocurrencia de un valor en el string.
  ```javascript
  console.log(saludo.indexOf("o")); // 1
  ```

- **`lastIndexOf()`**: Devuelve el índice de la última ocurrencia de un valor en el string.
  ```javascript
  console.log(saludo.lastIndexOf("o")); // 1
  ```

- **`length`**: Devuelve la longitud del string.
  ```javascript
  console.log(saludo.length); // 4
  ```

- **`match()`**: Busca un valor o expresión regular y devuelve las coincidencias.
  ```javascript
  console.log(saludo.match(/a/)); // ['a']
  ```

### Más Métodos de String
- **`repeat()`**: Devuelve un nuevo string con un número de copias del string original.
  ```javascript
  let risa = "ja";
  console.log(risa.repeat(3)); // jajaja
  ```

- **`replace()`**: Busca un patrón y devuelve un string donde la primera coincidencia es reemplazada.
  ```javascript
  let frase = "Hola mundo";
  console.log(frase.replace("mundo", "amigo")); // Hola amigo
  ```

- **`replaceAll()`**: Busca un patrón y devuelve un nuevo string donde todas las coincidencias son reemplazadas.
  ```javascript
  let texto = "Hola mundo, mundo";
  console.log(texto.replaceAll("mundo", "amigo")); // Hola amigo, amigo
  ```

- **`search()`**: Busca un valor o expresión regular y devuelve el índice de la coincidencia.
  ```javascript
  console.log(frase.search("mundo")); // 5
  ```

- **`slice()`**: Extrae una parte del string y devuelve un nuevo string.
  ```javascript
  console.log(frase.slice(0, 4)); // Hola
  ```

- **`split()`**: Divide un string en un array de subcadenas.
  ```javascript
  console.log(frase.split(" ")); // ["Hola", "mundo"]
  ```

- **`startsWith()`**: Comprueba si el string comienza con los caracteres especificados.
  ```javascript
  console.log(frase.startsWith("Hola")); // true
  ```

- **`substr()`**: Extrae un número de caracteres desde un índice específico.
  ```javascript
  console.log(frase.substr(0, 4)); // Hola
  ```

- **`substring()`**: Extrae caracteres entre dos índices especificados.
  ```javascript
  console.log(frase.substring(0, 4)); // Hola
  ```

### Métodos para Cambiar de MAYUSCULAS a minusculas
- **`toLowerCase()`**: Convierte el string a minúsculas.
  ```javascript
  console.log(frase.toLowerCase()); // hola mundo
  ```

- **`toUpperCase()`**: Convierte el string a mayúsculas.
  ```javascript
  console.log(frase.toUpperCase()); // HOLA MUNDO
  ```

- **`trim()`**: Elimina los espacios en blanco de ambos extremos del string.
  ```javascript
  let saludoEspacios = "  Hola  ";
  console.log(saludoEspacios.trim()); // Hola
  ```

- **`trimStart()`** y **`trimEnd()`**: Eliminan los espacios en blanco del inicio o del final del string respectivamente.
  ```javascript
  console.log(saludoEspacios.trimStart()); // "Hola  "
  console.log(saludoEspacios.trimEnd()); // "  Hola"
  ```

### Obtener el Valor Primitivo
- **`valueOf()`**: Devuelve el valor primitivo del objeto string.
  ```javascript
  let strObjeto = new String("Hola");
  console.log(strObjeto.valueOf()); // Hola
  