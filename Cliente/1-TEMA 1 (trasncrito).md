# JavaScript Fundamentals

## Índice
- Variables y tipos de datos
- Operadores
- Reglas para la coerción de tipos
- Let y el ámbito
- Problema con `var`
- `const`
- Strings
- Literales de plantilla (template literals)
- Condicionales
- Bucles
- Funciones
- Arrays
- Bucles `for`
- Parámetros por defecto
- Parámetro `rest`
- Operador `spread`
- Valores falsy
- Operador de coalición nula (`??`)

## Variables y Tipos de Datos

- Una variable es un espacio en blanco para almacenar un valor futuro.
- JavaScript usa varios tipos de valores:
  - Números y Booleanos (`true` o `false`)
  - Strings o secuencia de caracteres
  - Funciones
  - Arrays (listas de variables) y Objetos

### Tipos de Datos Primitivos
- **String**: Una secuencia de texto. Para indicar que el valor es un string, se encierra entre comillas simples o dobles.
  ```javascript
  let miVariable = 'Bob';
  let miVariable = "Bob";
  ```

- **Number**: Representa un número. Los números no llevan comillas.
  ```javascript
  let miVariable = 10;
  ```

- **Boolean**: Valor de verdadero (`true`) o falso (`false`). Estas palabras no llevan comillas.
  ```javascript
  let miVariable = true;
  ```

- **Array**: Una estructura que permite almacenar varios valores en una sola referencia.
  ```javascript
  let miVariable = [1, 'Bob', 'Steve', 10];
  // Acceder a cada miembro del array
  miVariable[0], miVariable[1], etc.
  ```

### Tipos Primitivos Especiales
- **null**: Representa valores desconocidos.
  ```javascript
  let valor = null;
  ```

- **undefined**: Representa valores no asignados.
  ```javascript
  let valor;
  console.log(valor); // undefined
  ```

### Objetos
- Para estructuras de datos más complejas. Todo en JavaScript es un objeto y se puede almacenar en una variable.
  ```javascript
  let miVariable = document.querySelector('h1');
  ```

## Variables
- Tipos primitivos: `undefined`, `number`, `string`, `boolean`, `function`, `object`.
  ```javascript
  let var1 = "Hola";
  console.log(typeof var1); // String
  let var2 = 25;
  console.log(typeof var2); // number
  let var3 = new Date();
  console.log(typeof var3); // Object
  let var4;
  console.log(typeof var4); // undefined
  let var5 = () => {};
  console.log(typeof var5); // function
  ```

- **Tipado débil y dinámico**:
  - Las variables tienen el tipo del último valor asignado.
  ```javascript
  let variable;
  console.log(typeof variable); // undefined
  variable = 25;
  console.log(typeof variable); // number
  variable = "hola";
  console.log(typeof variable); // string
```
## Operadores

### Tipos de Operadores
- **Adición**: Suma dos números o concatena dos strings.
  ```javascript
  let suma = 6 + 9;
  let concatenacion = 'Hola ' + 'mundo';
  ```

- **Resta, Multiplicación, División**: Operan de la forma esperada en matemáticas.
  ```javascript
  let resta = 9 - 3;
  let multiplicacion = 8 * 2; // Multiplicar se hace con un asterisco
  let division = 9 / 3;
  ```

- **Asignación**: Asigna un valor a una variable.
  ```javascript
  let miVariable = 'Bob';
  ```

- **Igualdad estricta**: Verifica si dos valores son iguales y del mismo tipo.
  ```javascript
  let miVariable = 3;
  console.log(miVariable === 4); // false
  ```

- **Negación y desigualdad**: Devuelven el valor lógicamente opuesto o verifican si dos valores no son iguales.
  ```javascript
  let miVariable = 3;
  console.log(!(miVariable === 3)); // false
  console.log(miVariable !== 3); // false
  ```

### Igualdad Relajada vs Estricta
- **Doble igual (`==`)**: Convierte los operandos al mismo tipo antes de compararlos.
  ```javascript
  const a = 100;
  const b = '100';
  console.log(a == b); // true
  ```

- **Triple igual (`===`)**: Compara los valores sin realizar conversión de tipos.
  ```javascript
  const a = 100;
  const b = '100';
  console.log(a === b); // false
  ```

- **Desigualdad relajada (`!=`)**: Verifica si dos valores no son iguales, intentando convertir los operandos al mismo tipo.
  ```javascript
  const a = 2;
  console.log(a != '2'); // false
  ```

- **Desigualdad estricta (`!==`)**: Verifica si dos valores no son iguales y si son de tipos diferentes.
  ```javascript
  const a = 2;
  console.log(a !== '2'); // true
  ```

## Reglas para la Coerción de Tipos
- Si uno de los operandos es un string, el otro será convertido a string.
- Si uno de los operandos es un número, el otro será convertido a número.
- Si uno de los operandos es un booleano, será convertido a número (`true` se convierte en `1` y `false` en `0`).
- Si un operando es un objeto y el otro es un valor primitivo, el objeto se convertirá a un valor primitivo antes de la comparación.
- Si uno de los operandos es `null` o `undefined`, el otro también debe ser `null` o `undefined` para devolver `true`. Caso contrario, devolverá `false`.

## Let y Ámbito

- `let` crea una variable con un ámbito definido.
- El ámbito es un término que define el límite donde las variables existen.
- El ámbito es cómo se asegura que el contenido dentro de una función no sea afectado por lo que está fuera de ella.
- El ámbito en JavaScript está principalmente definido por las llaves (`{}`).

### Ejemplo de Let y Ámbito
```javascript
let a = 50;
let b = 100;

if (true) {
   let a = 60;
   let c = 10;
   console.log(a / c); // 6
   console.log(b / c); // 10
}

console.log(a); // 50
console.log(c); // Error: c no está definido
```

- La variable `a` se encuentra tanto en el ámbito del script como en el ámbito del bloque `if`.
- La variable `a` dentro del bloque puede considerarse una variable diferente de la que está fuera del bloque.

## Problema con `var`

- Cuando se usa `var`, una variable puede ser redeclarada y actualizada.
- La redeclaración permite declarar más de una variable con el mismo nombre, lo que puede provocar errores inesperados si una variable se declara por error.

### Ejemplo de Problema con `var`
```javascript
var nombre = "mi nombre";
var miEdad = 22;

if (miEdad > 18) {
   var nombre = "otro nombre";
}

console.log(nombre); // salida: "otro nombre"
```
- En este caso, la variable `nombre` es redeclarada y modificada dentro del bloque `if`, afectando la variable global.

## `var` vs `let`

- **`var`**:
  - Permite redeclarar variables, incluso en diferentes ámbitos o bloques, lo que cambia el valor de la variable externa también.
  ```javascript
  var a = 5;
  console.log(a); // 5

  {
     var a = 3;
     console.log(a); // 3
  }

  console.log(a); // 3
  ```

- **`let`**:
  - Redeclarar una variable con `let` en un ámbito o bloque diferente la trata como una variable diferente.
  ```javascript
  let a = 5;
  console.log(a); // 5

  {
     let a = 3;
     console.log(a); // 3
  }

  console.log(a); // 5
  ```

- **Bucle con `var` vs `let`**:
  - Cuando se usa una variable declarada con `var` en un bucle, el valor de esa variable cambia fuera del bucle también.
  ```javascript
  var a = 2;
  for (var a = 0; a < 3; a++) {
     console.log('hola');
  }
  console.log(a); // 3
  ```
  - Cuando se usa `let`, el valor de la variable no cambia fuera del bucle.
  ```javascript
  let a = 2;
  for (let a = 0; a < 3; a++) {
     console.log('hola');
  }
  console.log(a); // 2
  ```

## `const`

- Hay ocasiones en las que no queremos que una variable cambie después de su asignación.
- Por ejemplo, si tienes una variable que representa el valor de `PI`, no querrías que cambie a lo largo del programa.

### Ejemplo de `const`
```javascript
const B = "Variable constante";
B = "Nuevo valor"; // muestra error

const LENGUAJES = ['Js', 'Ruby', 'Python', 'Go'];
LENGUAJES = "Javascript"; // muestra error

LENGUAJES.push('Java'); // Funciona
console.log(LENGUAJES); // ['Js', 'Ruby', 'Python', 'Go', 'Java']
```
- La variable `LENGUAJES` no puede ser cambiada, pero los elementos dentro del array sí pueden ser modificados si el array es mutable.
## Strings

- Los strings son cadenas de caracteres que se pueden definir con comillas simples, dobles o backticks.
  ```javascript
  let saludo = "Hola";
  let despedida = 'Adiós';
  let combinacion = `Combinando: ${saludo} y ${despedida}`;
  ```
- Las comillas simples y dobles son equivalentes, pero los backticks permiten la interpolación de variables y expresiones dentro del string, utilizando `${}`.

### Ejemplos de Strings
```javascript
let saludo = "Hola";
let despedida = 'Adiós';
let frase = `Esto es una frase con ${saludo} y ${despedida}`;
console.log(`1 + 2 = ${1 + 2}`); // 1 + 2 = 3
```
- Los backticks permiten la inclusión de expresiones directamente dentro del string.

## Literales de Plantilla (Template Literals)

- Los literales de plantilla permiten crear strings complejos sin necesidad de concatenación.
  ```javascript
  let nombre = "Juan";
  let edad = 30;
  let mensaje = `Hola, mi nombre es ${nombre} y tengo ${edad} años.`;
  console.log(mensaje); // Hola, mi nombre es Juan y tengo 30 años.
  ```
- También permiten escribir strings de múltiples líneas.
  ```javascript
  let multilinea = `Esta es una línea.
  Y esta es otra línea.`;
  console.log(multilinea);
  ```

## Condicionales

- Los condicionales se utilizan para tomar decisiones en el código.
  - **`if`**: Evalúa una condición, y si es verdadera, ejecuta el bloque de código.
  ```javascript
  let edad = 18;
  if (edad >= 18) {
    console.log("Eres mayor de edad");
  }
  ```
  - **`else`**: Proporciona una alternativa cuando la condición no se cumple.
  ```javascript
  let edad = 16;
  if (edad >= 18) {
    console.log("Eres mayor de edad");
  } else {
    console.log("Eres menor de edad");
  }
  ```
  - **`else if`**: Permite evaluar múltiples condiciones.
  ```javascript
  let temperatura = 25;
  if (temperatura > 30) {
    console.log("Hace mucho calor");
  } else if (temperatura < 15) {
    console.log("Hace frío");
  } else {
    console.log("El clima está agradable");
  }
  ```
- **Operador ternario**: Una forma abreviada de escribir condicionales simples.
  ```javascript
  let esAdulto = edad >= 18 ? "Sí, es adulto" : "No, es menor de edad";
  console.log(esAdulto);
  ```

## Bucles

- Los bucles se utilizan para repetir una sección de código varias veces.

### Bucle `for`
- Se utiliza cuando se conoce el número de iteraciones de antemano.
  ```javascript
  for (let i = 0; i < 5; i++) {
    console.log(`Iteración número ${i}`);
  }
  ```
- La estructura básica incluye una inicialización, una condición y una actualización.

### Bucle `while`
- Se utiliza cuando no se conoce el número exacto de iteraciones y se basa en una condición.
  ```javascript
  let contador = 0;
  while (contador < 5) {
    console.log(`Contador: ${contador}`);
    contador++;
  }
  ```

### Bucle `do...while`
- Similar al `while`, pero se ejecuta al menos una vez antes de evaluar la condición.
  ```javascript
  let numero = 0;
  do {
    console.log(`Número: ${numero}`);
    numero++;
  } while (numero < 5);
  ```

## Funciones

- Las funciones son bloques de código reutilizables que se pueden llamar en cualquier parte del programa.
- **Declaración de funciones**:
  ```javascript
  function saludar(nombre) {
    return `Hola, ${nombre}`;
  }
  console.log(saludar("Juan"));
  ```

### Tipos de Funciones
1. **Expresión de función**:
   ```javascript
   let sumar = function(a, b) {
     return a + b;
   };
   console.log(sumar(2, 3)); // 5
   ```

2. **Función flecha (Arrow Function)**:
   ```javascript
   let restar = (a, b) => a - b;
   console.log(restar(5, 3)); // 2
   ```
- Las funciones flecha son especialmente útiles para simplificar el código en funciones de una sola línea.

3. **Función inmediatamente invocada (IIFE)**:
   ```javascript
   (function() {
     console.log("Esto se ejecuta inmediatamente");
   })();
   ```

4. **Parámetros por defecto**: Permiten definir valores predeterminados para los parámetros de una función.
   ```javascript
   function multiplicar(a, b = 2) {
     return a * b;
   }
   console.log(multiplicar(5)); // 10
   ```

5. **Parámetro `rest`**: Permite a una función aceptar un número indefinido de argumentos como un array.
   ```javascript
   function sumarTodos(...numeros) {
     return numeros.reduce((acc, num) => acc + num, 0);
   }
   console.log(sumarTodos(1, 2, 3, 4)); // 10
   ```

6. **Operador `spread`**: Expande los elementos de un array u objeto.
   ```javascript
   let numeros = [1, 2, 3];
   let otrosNumeros = [...numeros, 4, 5];
   console.log(otrosNumeros); // [1, 2, 3, 4, 5]
   ```

## Arrays

- Los arrays son estructuras que permiten almacenar múltiples valores en una sola variable.
- Se pueden crear usando corchetes `[]`.
  ```javascript
  let frutas = ["manzana", "plátano", "naranja"];
  console.log(frutas[0]); // manzana
  console.log(frutas.length); // 3
  ```

### Métodos Comunes de Arrays

1. **`push()`**: Añade un elemento al final del array.
   ```javascript
   frutas.push("uva");
   console.log(frutas); // ["manzana", "plátano", "naranja", "uva"]
   ```

2. **`pop()`**: Elimina el último elemento del array.
   ```javascript
   frutas.pop();
   console.log(frutas); // ["manzana", "plátano", "naranja"]
   ```

3. **`shift()`**: Elimina el primer elemento del array.
   ```javascript
   frutas.shift();
   console.log(frutas); // ["plátano", "naranja"]
   ```

4. **`unshift()`**: Añade un elemento al inicio del array.
   ```javascript
   frutas.unshift("fresa");
   console.log(frutas); // ["fresa", "plátano", "naranja"]
   ```

5. **`map()`**: Crea un nuevo array con los resultados de aplicar una función a cada elemento del array.
   ```javascript
   let numeros = [1, 2, 3, 4];
   let dobles = numeros.map(num => num * 2);
   console.log(dobles); // [2, 4, 6, 8]
   ```

6. **`filter()`**: Crea un nuevo array con todos los elementos que cumplan una condición.
   ```javascript
   let mayores = numeros.filter(num => num > 2);
   console.log(mayores); // [3, 4]
   ```

7. **`reduce()`**: Aplica una función a un acumulador y a cada elemento del array para reducirlo a un único valor.
   ```javascript
   let suma = numeros.reduce((acumulador, num) => acumulador + num, 0);
   console.log(suma); // 10
   ```

8. **`forEach()`**: Ejecuta una función para cada elemento del array.
   ```javascript
   numeros.forEach(num => console.log(num));
   // 1
   // 2
   // 3
   // 4
   ```

## Valores Falsy

- En JavaScript, algunos valores son considerados "falsy", lo que significa que se evalúan como `false` en un contexto booleano.
- Los valores "falsy" son:
  - `false`
  - `0`
  - `""` (cadena vacía)
  - `null`
  - `undefined`
  - `NaN` (Not-a-Number)

### Ejemplo de Valores Falsy
```javascript
if (false || 0 || "" || null || undefined || NaN) {
  console.log("Esto no se ejecutará");
} else {
  console.log("Todos estos valores son falsy");
}
// Salida: Todos estos valores son falsy
```

## Operador de Coalición Nula (`??`)

- El operador `??` devuelve el operando de la derecha cuando el operando de la izquierda es `null` o `undefined`.
- Es útil para proporcionar valores predeterminados cuando una variable puede ser `null` o `undefined`.

### Ejemplo del Operador de Coalición Nula
```javascript
let altura = 0;
console.log(altura || 100); // 100 (porque 0 es falsy)
console.log(altura ?? 100); // 0 (porque `altura` no es null ni undefined)

let nombre;
console.log(nombre ?? "Anónimo"); // Anónimo (porque `nombre` es undefined)
```

## Desestructuración

- La desestructuración permite extraer valores de arrays u objetos y asignarlos a variables de forma más conveniente.

### Desestructuración de Arrays
```javascript
let colores = ["rojo", "verde", "azul"];
let [primero, segundo] = colores;
console.log(primero); // rojo
console.log(segundo); // verde
```
- También se pueden omitir elementos del array.
  ```javascript
  let [primero, , tercero] = colores;
  console.log(tercero); // azul
  ```

### Desestructuración de Objetos
```javascript
let persona = { nombre: "Juan", edad: 30 };
let { nombre, edad } = persona;
console.log(nombre); // Juan
console.log(edad); // 30
```
- Se pueden renombrar las variables durante la desestructuración.
  ```javascript
  let { nombre: nombrePersona, edad: edadPersona } = persona;
  console.log(nombrePersona); // Juan
  console.log(edadPersona); // 30
  ```
## Spread Operator (`...`)

- El operador `spread` se utiliza para expandir los elementos de un array u objeto en lugares donde se esperan múltiples elementos.

### Ejemplo de Spread con Arrays
```javascript
let numeros = [1, 2, 3];
let nuevosNumeros = [...numeros, 4, 5];
console.log(nuevosNumeros); // [1, 2, 3, 4, 5]
```

- También se puede usar para combinar arrays.
  ```javascript
  let array1 = ["a", "b"];
  let array2 = ["c", "d"];
  let combinado = [...array1, ...array2];
  console.log(combinado); // ["a", "b", "c", "d"]
  ```

### Ejemplo de Spread con Objetos
```javascript
let objeto1 = { a: 1, b: 2 };
let objeto2 = { c: 3, d: 4 };
let combinadoObjeto = { ...objeto1, ...objeto2 };
console.log(combinadoObjeto); // { a: 1, b: 2, c: 3, d: 4 }
```

## Rest Parameter (`...`)

- El parámetro `rest` permite a una función aceptar un número indefinido de argumentos como un array.

### Ejemplo del Parámetro `rest`
```javascript
function sumarTodos(...numeros) {
  return numeros.reduce((acumulador, num) => acumulador + num, 0);
}
console.log(sumarTodos(1, 2, 3, 4)); // 10
```
- Los parámetros `rest` deben ser los últimos parámetros en una función.



# CONTENIDO EXTRA
## Manejo de Errores

- JavaScript proporciona `try...catch` para manejar errores y evitar que el programa se detenga de manera inesperada.

### Ejemplo de `try...catch`
```javascript
try {
  let resultado = noDefinido + 1; // Esto generará un error
} catch (error) {
  console.log("Ha ocurrido un error: " + error.message);
}
// Salida: Ha ocurrido un error: noDefinido is not defined
```

- También se puede usar `finally` para ejecutar código independientemente de si hubo un error o no.
  ```javascript
  try {
    let resultado = 10 / 2;
    console.log(resultado);
  } catch (error) {
    console.log("Error: " + error.message);
  } finally {
    console.log("Esto se ejecuta siempre");
  }
  // Salida:
  // 5
  // Esto se ejecuta siempre
  ```

## Clases

- Las clases en JavaScript son una forma de crear objetos y definir su comportamiento.

### Definición de una Clase
```javascript
class Persona {
  constructor(nombre, edad) {
    this.nombre = nombre;
    this.edad = edad;
  }

  saludar() {
    console.log(`Hola, mi nombre es ${this.nombre} y tengo ${this.edad} años.`);
  }
}

let juan = new Persona("Juan", 30);
juan.saludar(); // Hola, mi nombre es Juan y tengo 30 años.
```

- Las clases pueden tener métodos como `constructor` para inicializar propiedades y otros métodos para definir comportamientos.

### Herencia de Clases
- Se pueden crear clases que hereden de otras clases usando `extends`.
  ```javascript
  class Estudiante extends Persona {
    constructor(nombre, edad, grado) {
      super(nombre, edad);
      this.grado = grado;
    }

    estudiar() {
      console.log(`${this.nombre} está estudiando en el grado ${this.grado}.`);
    }
  }

  let pedro = new Estudiante("Pedro", 20, "10º");
  pedro.saludar(); // Hola, mi nombre es Pedro y tengo 20 años.
  pedro.estudiar(); // Pedro está estudiando en el grado 10º.
  ```

## Promesas

- Las promesas son objetos que representan la finalización (o falla) de una operación asíncrona y su valor resultante.

### Ejemplo de Promesa
```javascript
let promesa = new Promise((resolve, reject) => {
  let exito = true;
  if (exito) {
    resolve("La operación fue exitosa");
  } else {
    reject("Hubo un error en la operación");
  }
});

promesa
  .then(resultado => console.log(resultado)) // La operación fue exitosa
  .catch(error => console.log(error));
```
- Las promesas tienen métodos `then` para manejar el resultado y `catch` para manejar errores.

## `async` / `await`

- `async` / `await` es una sintaxis para manejar promesas de manera más fácil y legible.
- Una función marcada con `async` devuelve siempre una promesa.

### Ejemplo de `async` / `await`
```javascript
async function obtenerDatos() {
  try {
    let respuesta = await fetch("https://api.example.com/datos");
    let datos = await respuesta.json();
    console.log(datos);
  } catch (error) {
    console.log("Error: " + error.message);
  }
}

obtenerDatos();
```
- `await` solo se puede usar dentro de funciones `async` y pausa la ejecución hasta que la promesa se resuelve.
  
  
  

## Operadores Lógicos y Comparación

- Los operadores lógicos y de comparación se utilizan para evaluar condiciones y realizar decisiones en el flujo del programa.

### Operadores de Comparación
- **Igualdad (`==`)**: Compara dos valores para ver si son iguales, realizando una conversión de tipos si es necesario.
  ```javascript
  console.log(5 == "5"); // true
  ```

- **Igualdad estricta (`===`)**: Compara dos valores sin realizar conversión de tipos.
  ```javascript
  console.log(5 === "5"); // false
  ```

- **Desigualdad (`!=`)**: Compara si dos valores son diferentes, realizando una conversión de tipos si es necesario.
  ```javascript
  console.log(5 != "5"); // false
  ```

- **Desigualdad estricta (`!==`)**: Compara si dos valores son diferentes sin realizar conversión de tipos.
  ```javascript
  console.log(5 !== "5"); // true
  ```

- **Mayor que (`>`)**, **Mayor o igual que (`>=`)**, **Menor que (`<`)**, **Menor o igual que (`<=`)**: Se utilizan para comparar valores numéricos.
  ```javascript
  console.log(10 > 5); // true
  console.log(10 <= 5); // false
  ```

### Operadores Lógicos
- **AND (`&&`)**: Devuelve `true` solo si ambas condiciones son verdaderas.
  ```javascript
  console.log(true && false); // false
  console.log(true && true); // true
  ```

- **OR (`||`)**: Devuelve `true` si al menos una de las condiciones es verdadera.
  ```javascript
  console.log(true || false); // true
  console.log(false || false); // false
  ```

- **NOT (`!`)**: Invierte el valor de verdad.
  ```javascript
  console.log(!true); // false
  console.log(!false); // true
  ```

## JSON (JavaScript Object Notation)

- **JSON** es un formato ligero de intercambio de datos, fácil de leer y escribir para humanos, y fácil de analizar y generar para las máquinas.

### Ejemplo de JSON
```json
{
  "nombre": "Juan",
  "edad": 30,
  "activo": true,
  "hobbies": ["fútbol", "lectura", "ciclismo"]
}
```

### Conversión entre JSON y Objetos JavaScript
- **`JSON.stringify()`**: Convierte un objeto JavaScript a una cadena JSON.
  ```javascript
  let objeto = { nombre: "Juan", edad: 30 };
  let json = JSON.stringify(objeto);
  console.log(json); // "{"nombre":"Juan","edad":30}"
  ```

- **`JSON.parse()`**: Convierte una cadena JSON a un objeto JavaScript.
  ```javascript
  let jsonString = '{"nombre": "Juan", "edad": 30}';
  let objetoParseado = JSON.parse(jsonString);
  console.log(objetoParseado.nombre); // Juan
  ```

## Manipulación del DOM

- El **DOM (Document Object Model)** es la representación estructurada de un documento HTML. JavaScript permite manipular el DOM para cambiar dinámicamente el contenido de una página web.

### Selección de Elementos
- **`document.getElementById()`**: Selecciona un elemento por su ID.
  ```javascript
  let elemento = document.getElementById("miElemento");
  ```

- **`document.querySelector()`**: Selecciona el primer elemento que coincide con el selector CSS proporcionado.
  ```javascript
  let elemento = document.querySelector(".clase");
  ```

- **`document.querySelectorAll()`**: Selecciona todos los elementos que coinciden con el selector CSS proporcionado.
  ```javascript
  let elementos = document.querySelectorAll("div");
  ```

### Manipulación de Elementos
- **`innerHTML`**: Cambia el contenido HTML interno de un elemento.
  ```javascript
  let div = document.getElementById("miDiv");
  div.innerHTML = "<p>Nuevo contenido</p>";
  ```

- **`textContent`**: Cambia solo el texto de un elemento.
  ```javascript
  div.textContent = "Nuevo texto";
  ```

- **`setAttribute()`**: Cambia o añade un atributo al elemento.
  ```javascript
  div.setAttribute("class", "nuevaClase");
  ```

### Creación y Eliminación de Elementos
- **`createElement()`**: Crea un nuevo elemento HTML.
  ```javascript
  let nuevoParrafo = document.createElement("p");
  nuevoParrafo.textContent = "Este es un nuevo párrafo";
  ```

- **`appendChild()`**: Añade un elemento hijo al elemento especificado.
  ```javascript
  div.appendChild(nuevoParrafo);
  ```

- **`removeChild()`**: Elimina un elemento hijo del elemento especificado.
  ```javascript
  div.removeChild(nuevoParrafo);
  ```

## Eventos

- Los **eventos** permiten que JavaScript responda a interacciones del usuario, como hacer clic en un botón o mover el ratón.

### Ejemplo de Evento `click`
```javascript
let boton = document.getElementById("miBoton");

boton.addEventListener("click", () => {
  alert("¡Botón clickeado!");
});
```
- **`addEventListener()`** se usa para asociar una función a un evento específico en un elemento.

## `this`

- **`this`** es una referencia al objeto actual en el contexto en el que se está ejecutando el código.
- En el contexto de un método de un objeto, **`this`** hace referencia al propio objeto.

### Ejemplo de `this`
```javascript
let coche = {
  marca: "Toyota",
  modelo: "Corolla",
  mostrarInfo: function() {
    console.log(`Coche: ${this.marca} ${this.modelo}`);
  }
};

coche.mostrarInfo(); // Coche: Toyota Corolla
```
- En este caso, **`this`** se refiere al objeto `coche` dentro del método `mostrarInfo`.
  
  # JavaScript Fundamentals

## Prototipos y Herencia Prototípica

- En JavaScript, cada objeto tiene un prototipo del cual hereda propiedades y métodos. Esto se llama **herencia prototípica**.
- Los prototipos permiten compartir métodos y propiedades entre múltiples objetos, haciendo el código más eficiente.

### Creación de Prototipos
- Puedes agregar métodos a un objeto usando la propiedad `prototype`.
  ```javascript
  function Persona(nombre, edad) {
    this.nombre = nombre;
    this.edad = edad;
  }

  Persona.prototype.saludar = function() {
    console.log(`Hola, me llamo ${this.nombre} y tengo ${this.edad} años.`);
  };

  let juan = new Persona("Juan", 25);
  juan.saludar(); // Hola, me llamo Juan y tengo 25 años.
  ```

- En el ejemplo anterior, `saludar` se define en el prototipo de `Persona`, por lo que todas las instancias de `Persona` comparten el mismo método `saludar`.

## Funciones Constructoras

- Las **funciones constructoras** se utilizan para crear objetos múltiples con las mismas propiedades y métodos.
- Por convención, las funciones constructoras comienzan con una letra mayúscula.
  ```javascript
  function Coche(marca, modelo) {
    this.marca = marca;
    this.modelo = modelo;
  }

  let miCoche = new Coche("Toyota", "Corolla");
  console.log(miCoche.marca); // Toyota
  ```

- Al usar `new` con una función constructora, se crea un nuevo objeto y se asigna el prototipo correspondiente.

## Clases vs. Prototipos

- Las **clases** son una sintaxis más moderna introducida en ECMAScript 6 (ES6) que hace que el uso de prototipos sea más sencillo y claro.
- Las clases en JavaScript son básicamente una envoltura para la herencia prototípica, y no cambian cómo funciona JavaScript a nivel fundamental.
  ```javascript
  class Animal {
    constructor(nombre) {
      this.nombre = nombre;
    }

    hacerSonido() {
      console.log(`${this.nombre} hace un sonido.`);
    }
  }

  let perro = new Animal("Perro");
  perro.hacerSonido(); // Perro hace un sonido.
  ```

- Las clases simplifican la herencia y permiten la creación de objetos de una manera más familiar para programadores que vienen de otros lenguajes orientados a objetos.

## Asincronía y el Event Loop

- JavaScript es un lenguaje **single-threaded**, lo que significa que solo puede ejecutar una cosa a la vez. Sin embargo, puede gestionar operaciones asíncronas a través del **event loop**.
- El **event loop** es un mecanismo que permite a JavaScript realizar tareas asíncronas, como solicitudes HTTP, al mismo tiempo que sigue ejecutando otros fragmentos de código.

### Callbacks
- Los **callbacks** son funciones que se pasan como argumentos a otras funciones y se ejecutan después de que la tarea principal ha finalizado.
  ```javascript
  function hacerAlgoImportante(callback) {
    console.log("Haciendo algo importante...");
    callback();
  }

  function finalizar() {
    console.log("Tarea finalizada.");
  }

  hacerAlgoImportante(finalizar);
  // Haciendo algo importante...
  // Tarea finalizada.
  ```

### Promesas
- Las **promesas** son una forma de manejar la asincronía de manera más clara y limpia que con los callbacks anidados.
- Una promesa tiene tres estados posibles: **pendiente**, **resuelta** y **rechazada**.
  ```javascript
  let promesa = new Promise((resolve, reject) => {
    let exito = true;
    if (exito) {
      resolve("Operación exitosa");
    } else {
      reject("Hubo un error");
    }
  });

  promesa
    .then((resultado) => console.log(resultado))
    .catch((error) => console.log(error));
  ```

### `async` / `await`
- `async` y `await` simplifican la escritura de código asíncrono.
- `await` hace que la función espere hasta que la promesa se resuelva, sin bloquear el hilo principal.
  ```javascript
  async function obtenerDatos() {
    try {
      let respuesta = await fetch("https://api.example.com/datos");
      let datos = await respuesta.json();
      console.log(datos);
    } catch (error) {
      console.log("Error: " + error.message);
    }
  }

  obtenerDatos();
  ```

## AJAX y Fetch API

- **AJAX** (Asynchronous JavaScript and XML) permite actualizar partes de una página web sin tener que recargar toda la página.
- **Fetch API** es una alternativa moderna a `XMLHttpRequest` para hacer solicitudes HTTP.

### Ejemplo de Fetch API
```javascript
fetch("https://api.example.com/datos")
  .then((respuesta) => {
    if (!respuesta.ok) {
      throw new Error("Error en la solicitud");
    }
    return respuesta.json();
  })
  .then((datos) => console.log(datos))
  .catch((error) => console.log("Error: " + error.message));
```

- `fetch` devuelve una promesa que se resuelve con la respuesta de la solicitud. Puedes manejar la respuesta y los errores con `.then()` y `.catch()`.