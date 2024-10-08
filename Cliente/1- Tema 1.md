## **Índice**

[[#**Sección 1 Variables y Tipos de Datos**]]
[[#**Sección 2 Operadores**]]
[[#**Sección 3 Reglas de Coerción de Tipos**]]
[[#**Sección 4 Ámbito de Variables (let y var)**]]
[[#**Sección 5 Constantes (const)**]]
[[#**5.1 Declaración de Constantes**]
[[#**Sección 6 Strings (Cadenas de Texto)**]]
[[#**Sección 7 Estructuras de Control**]]
[[#**8.1 Definición de Funciones**]]
[[#**Sección 9 Funciones de Flecha (Arrow Functions)**]]
[[#**Sección 10 Arrays (Arreglos)**]]
[[#**Sección 11 Bucles con Arrays**]]
[[#**Sección 12 Características Avanzadas de Funciones y Arrays**]]

## **Sección 1: Variables y Tipos de Datos**

### **1.1-Introducción-a-las-Variables**
Una **variable** es un contenedor que permite almacenar valores, los cuales pueden ser utilizados y modificados durante la ejecución de un programa. En JavaScript, una variable se declara utilizando las palabras clave `var`, `let` o `const`.

**[⬆ Volver al índice](#índice)**

### **1.2 Tipos de Datos Primitivos**
Los **tipos de datos primitivos** en JavaScript son los tipos básicos que representan un solo valor:
- **Números**: Incluyen enteros y decimales, por ejemplo `42` o `3.14`.
- **Booleanos**: Valores lógicos `true` o `false`.
- **Strings**: Cadenas de texto, como `"Hola Mundo"`.
- **Undefined**: Representa una variable que ha sido declarada pero no se le ha asignado ningún valor.
- **Null**: Representa la ausencia intencionada de un valor.

**Ejemplos de Declaración y Asignación**:
```js
let numero = 42;
let texto = "Hola";
let esVerdadero = true;
```

**[⬆ Volver al índice](#índice)**

### **1.3 Tipos de Datos Especiales**
- **Null**: Un valor especial que indica un valor desconocido o vacío. Ejemplo:
  ```js
  let valor = null;
  ```
- **Undefined**: Se refiere a una variable que ha sido declarada pero aún no tiene un valor asignado. Ejemplo:
  ```js
  let sinAsignar;
  console.log(sinAsignar); // undefined
  ```

**[⬆ Volver al índice](#índice)**

### **1.4 Tipos de Datos Objeto**
Un **objeto** es una colección de pares clave-valor, y puede contener múltiples tipos de datos, incluyendo otros objetos. Son estructuras complejas utilizadas para representar entidades.

Ejemplo:
```js
let persona = {
  nombre: "Juan",
  edad: 30
};
```

**[⬆ Volver al índice](#índice)**

### **1.5 Tipado Dinámico en JavaScript**
JavaScript tiene **tipado dinámico**, lo que significa que una variable puede cambiar de tipo según el valor que se le asigne. Ejemplo:
```js
let ejemplo = 42;      // Número
ejemplo = "Hola";    // String
ejemplo = true;       // Booleano
```

**[⬆ Volver al índice](#índice)**

## **Sección 2: Operadores**

### **2.1 Operadores Aritméticos**
Los **operadores aritméticos** se usan para realizar operaciones matemáticas:
- **Suma (+)**: `5 + 3 // 8`
- **Resta (-)**: `5 - 3 // 2`
- **Multiplicación (*)**: `5 * 3 // 15`
- **División (/)**: `6 / 3 // 2`
- **Módulo (%)**: `5 % 2 // 1`

**[⬆ Volver al índice](#índice)**

### **2.2 Operador de Asignación**
El **operador de asignación (`=`)** se utiliza para asignar valores a variables. Ejemplo:
```js
let x = 10;
```
### **2.3 Operadores de Comparación**
Los **operadores de comparación** se usan para comparar valores:
- **Igualdad (`==`)**: Compara sin tener en cuenta el tipo.
- **Igualdad estricta (`===`)**: Compara valor y tipo.
- **Desigualdad (`!=`)**: Diferente sin tener en cuenta el tipo.
- **Desigualdad estricta (`!==`)**: Diferente valor o tipo.
- **Mayor (`>`)**, **Menor (`<`)**, **Mayor o igual (`>=`)**, **Menor o igual (`<=`)**.

Ejemplo:
```js
5 == '5' // true
5 === '5' // false
```

**[⬆ Volver al índice](#índice)**

### **2.4 Operadores Lógicos**
- **AND (`&&`)**: Devuelve `true` si ambas expresiones son `true`.
- **OR (`||`)**: Devuelve `true` si al menos una expresión es `true`.
- **NOT (`!`)**: Niega el valor booleano.

Ejemplo:
```js
let a = true;
let b = false;
console.log(a && b); // false
console.log(a || b); // true
console.log(!a);     // false
```

**[⬆ Volver al índice](#índice)**

## **Sección 3: Reglas de Coerción de Tipos**

### **3.1 Introducción a la Coerción de Tipos**
La **coerción de tipos** es el proceso mediante el cual JavaScript convierte automáticamente los tipos de datos de una variable para que la operación tenga sentido. Puede ocurrir tanto de forma implícita como explícita.

Ejemplo:
```js
let resultado = '5' + 2; // '52' (coerción implícita a string)
```

**[⬆ Volver al índice](#índice)**

### **3.2 Reglas de Conversión**
JavaScript sigue reglas específicas para la **conversión de tipos** en operaciones con diferentes tipos de datos:
- **String + Número**: Convierte el número a string y concatena.
- **Booleano a Número**: `true` se convierte a `1` y `false` a `0`.
- **String a Número**: JavaScript intentará convertir el string a número si es posible.

Ejemplo:
```js
console.log('5' * 2); // 10 (coerción implícita a número)
```

**[⬆ Volver al índice](#índice)**

## **Sección 4: Ámbito de Variables (let y var)**

### **4.1 Introducción al Ámbito (Scope)**
El **ámbito** determina dónde se puede acceder a una variable dentro del código. JavaScript tiene tres tipos principales de ámbito:
- **Ámbito Global**: Las variables declaradas fuera de cualquier función tienen un ámbito global.
- **Ámbito de Función**: Las variables declaradas dentro de una función son accesibles solo dentro de esa función.
- **Ámbito de Bloque**: Introducido con `let` y `const`, las variables tienen ámbito de bloque, es decir, son accesibles solo dentro del bloque `{}` donde se declaran.

**[⬆ Volver al índice](#índice)**

### **4.2 Declaración de Variables con let**
La palabra clave **`let`** permite declarar variables con **ámbito de bloque**, lo cual ayuda a evitar problemas con la redeclaración de variables.

Ejemplo:
```js
if (true) {
  let mensaje = "Hola";
  console.log(mensaje); // Hola
}
console.log(mensaje); // Error: mensaje no está definido
```

**[⬆ Volver al índice](#índice)**

### **4.3 Problemas con var**
Antes de `let`, se usaba **`var`** para declarar variables, pero esto presentaba problemas debido a su **ámbito global o de función**. Las variables declaradas con `var` se pueden acceder fuera de su bloque, lo cual puede causar comportamientos inesperados.

Ejemplo:
```js
if (true) {
  var mensaje = "Hola";
}
console.log(mensaje); // Hola (mensaje es accesible fuera del bloque)
```

**[⬆ Volver al índice](#índice)**

## **Sección 5: Constantes (const)**

### **5.1 Declaración de Constantes**
La palabra clave **`const`** se usa para declarar **constantes**, es decir, valores que no se pueden reasignar después de ser inicializados. Sin embargo, si el valor es un objeto, sus propiedades **sí** se pueden modificar.

Ejemplo:
```js
const nombre = "Juan";
// nombre = "Pedro"; // Error: No se puede reasignar

const persona = { nombre: "Juan" };
persona.edad = 30; // Esto es válido
```

**[⬆ Volver al índice](#índice)**

## **Sección 6: Strings (Cadenas de Texto)**

### **6.1 Manipulación de Strings**
Los **strings** se pueden crear utilizando comillas simples (`'`), comillas dobles (`"`) o **template literals** (`` ` ``). Los **template literals** permiten la **interpolación de variables** y la creación de **strings multilínea**.

Ejemplo:
```js
let nombre = "Juan";
let saludo = `Hola, ${nombre}`; // Interpolación de variables
console.log(saludo); // Hola, Juan

let textoMultilinea = `Este es un texto
que ocupa varias líneas.`;
console.log(textoMultilinea);
```

**[⬆ Volver al índice](#índice)**

## **Sección 7: Estructuras de Control**

### **7.1 Condicionales**
Las **sentencias condicionales** permiten ejecutar diferentes bloques de código basándose en condiciones. En JavaScript se utilizan `if`, `else if` y `else` para controlar el flujo.

Ejemplo:
```js
let edad = 18;
if (edad < 18) {
  console.log("Eres menor de edad");
} else if (edad === 18) {
  console.log("Tienes 18 años");
} else {
  console.log("Eres mayor de edad");
}
```

**[⬆ Volver al índice](#índice)**

### **7.2 Bucles (while y do...while)**
Los **bucles** permiten repetir un bloque de código mientras una condición sea verdadera.
- **`while`**: Ejecuta el bloque mientras la condición sea verdadera.
- **`do...while`**: Ejecuta el bloque al menos una vez, y luego continúa si la condición es verdadera.

Ejemplo:
```js
let i = 0;
while (i < 5) {
  console.log(i);
  i++;
}

do {
  console.log(i);
  i++;
} while (i < 10);
```

**[⬆ Volver al índice](#índice)**

## **Sección 8: Funciones**

### **8.1 Definición de Funciones**
Una **función** es un bloque de código reutilizable que se puede ejecutar en cualquier momento. Se declara con la palabra clave `function`.

Ejemplo:
```js
function saludar() {
  console.log("Hola Mundo");
}
```

**[⬆ Volver al índice](#índice)**

### **8.2 Invocación de Funciones**
Para **llamar** a una función y ejecutar su código, se usa su nombre seguido de paréntesis.

Ejemplo:
```js
saludar(); // Hola Mundo
```

**[⬆ Volver al índice](#índice)**

### **8.3 Retorno de Valores**
Las funciones pueden devolver un valor usando la palabra clave **`return`**.

Ejemplo:
```js
function sumar(a, b) {
  return a + b;
}
let resultado = sumar(5, 3); // 8
```

**[⬆ Volver al índice](#índice)**

## **Sección 9: Funciones de Flecha (Arrow Functions)**

### **9.1 Nueva Sintaxis de Funciones**
Las **funciones de flecha** son una forma más concisa de escribir funciones en JavaScript. Utilizan la sintaxis `=>`.

Ejemplo:
```js
const saludar = () => {
  console.log("Hola Mundo");
};
```

**[⬆ Volver al índice](#índice)**

### **9.2 Ámbito y Funciones de Flecha**
Las **funciones de flecha** no tienen su propio valor de `this`, sino que heredan el valor de `this` del contexto en el que fueron definidas, lo cual las hace útiles en ciertos casos donde el ámbito de `this` es importante.

Ejemplo:
```js
function Persona() {
  this.edad = 0;
  setInterval(() => {
    this.edad++; // `this` hace referencia a Persona
  }, 1000);
}
```

**[⬆ Volver al índice](#índice)**

### **9.3 Tipos de Funciones de Flecha**
Las funciones de flecha pueden escribirse sin llaves `{}` si el cuerpo de la función tiene una sola línea y devuelve un valor. Si se usan llaves, es necesario incluir la palabra clave `return`.

Ejemplo:
```js
const sumar = (a, b) => a + b; // Retorno implícito

const restar = (a, b) => {
  return a - b; // Uso de llaves y retorno explícito
};
```

**[⬆ Volver al índice](#índice)**

## **Sección 10: Arrays (Arreglos)**

### **10.1 Introducción a los Arrays**
Los **arrays** son estructuras de datos utilizadas para almacenar **colecciones ordenadas** de valores. Cada valor tiene un **índice**, empezando desde `0`.

Ejemplo:
```js
let frutas = ["Manzana", "Banana", "Cereza"];
```

**[⬆ Volver al índice](#índice)**

### **10.2 Acceso a Elementos**
Puedes acceder a los **elementos** de un array usando su índice.

Ejemplo:
```js
let primeraFruta = frutas[0]; // "Manzana"
```

**[⬆ Volver al índice](#índice)**

### **10.3 Propiedades y Métodos de Arrays**
- **`.length`**: Devuelve la longitud del array.
- **`.push()`**: Añade un elemento al final del array.
- **`.pop()`**: Elimina el último elemento del array.
- **`.shift()`**: Elimina el primer elemento del array.
- **`.unshift()`**: Añade un elemento al inicio del array.
- **`.map()`**: Crea un nuevo array con los resultados de aplicar una función a cada elemento.
- **`.filter()`**: Crea un nuevo array con los elementos que cumplen una condición.
- **`.reduce()`**: Aplica una función a un acumulador y a cada valor del array para reducirlo a un solo valor.

Ejemplo:
```js
let numeros = [1, 2, 3, 4];
let cuadrados = numeros.map(num => num * num); // [1, 4, 9, 16]
```

**[⬆ Volver al índice](#índice)**

## **Sección 11: Bucles con Arrays**

### **11.1 Bucle for**
El **bucle `for`** se utiliza para iterar sobre los elementos de un array de forma tradicional, con un contador que se incrementa en cada iteración.

Ejemplo:
```js
let numeros = [1, 2, 3, 4, 5];
for (let i = 0; i < numeros.length; i++) {
  console.log(numeros[i]);
}
```

**[⬆ Volver al índice](#índice)**

### **11.2 Bucle for...of**
El **bucle `for...of`** proporciona una forma más sencilla y legible de iterar sobre los valores de un array.

Ejemplo:
```js
let frutas = ["Manzana", "Banana", "Cereza"];
for (let fruta of frutas) {
  console.log(fruta);
}
```

**[⬆ Volver al índice](#índice)**

### **11.3 Bucle forEach**
El método **`.forEach()`** permite ejecutar una función específica por cada elemento del array, pasando el elemento actual como argumento.

Ejemplo:
```js
let numeros = [1, 2, 3, 4, 5];
numeros.forEach(numero => {
  console.log(numero);
});
```

**[⬆ Volver al índice](#índice)**

### **11.4 Diferencias entre for...in y for...of**
- **`for...in`**: Itera sobre las **propiedades** de un objeto, incluyendo las propiedades heredadas del prototipo. No se recomienda para arrays, ya que puede devolver índices inesperados.
- **`for...of`**: Itera sobre los **valores** de un array u otra colección iterable, siendo más adecuado para recorrer arrays.

Ejemplo:
```js
let array = ["a", "b", "c"];
for (let index in array) {
  console.log(index); // Muestra los índices: 0, 1, 2
}
for (let value of array) {
  console.log(value); // Muestra los valores: "a", "b", "c"
}
```

**[⬆ Volver al índice](#índice)**

## **Sección 12: Características Avanzadas de Funciones y Arrays**

### **12.1 Desestructuración de Arrays**
La **desestructuración de arrays** permite extraer valores del array y asignarlos a variables individuales de forma más concisa.

Ejemplo:
```js
let colores = ["rojo", "verde", "azul"];
let [primero, segundo, tercero] = colores;
console.log(primero); // "rojo"
console.log(segundo); // "verde"
```

**[⬆ Volver al índice](#índice)**

### **12.2 Clonación de Arrays**
Existen varias formas de **clonar** un array, creando una copia superficial del mismo:
- **Operador Spread (`...`)**:
  ```js
  let original = [1, 2, 3];
  let copia = [...original];
  ```
- **Método `Array.from()`**:
  ```js
  let copia = Array.from(original);
  ```
- **Método `slice()`**:
  ```js
  let copia = original.slice();
  ```

**[⬆ Volver al índice](#índice)**

### **12.3 Parámetros por Defecto**
Los **parámetros por defecto** permiten que una función tenga valores predefinidos en caso de que no se proporcionen argumentos al llamarla.

Ejemplo:
```js
function saludar(nombre = "Amigo") {
  console.log(`Hola, ${nombre}!`);
}
saludar(); // "Hola, Amigo!"
saludar("Juan"); // "Hola, Juan!"
```

**[⬆ Volver al índice](#índice)**

### **12.4 Parámetro Rest (`...`)**
El **parámetro rest** permite a una función aceptar un número variable de argumentos, que son convertidos en un array.

Ejemplo:
```js
function sumar(...numeros) {
  return numeros.reduce((acumulado, actual) => acumulado + actual, 0);
}
console.log(sumar(1, 2, 3)); // 6
```

**[⬆ Volver al índice](#índice)**

### **12.5 Operador Spread (`...`)**
El **operador spread** se utiliza para **expandir** elementos de un array en otro array o como argumentos en una función.

Ejemplo:
```js
let numeros = [1, 2, 3];
let masNumeros = [...numeros, 4, 5, 6];
console.log(masNumeros); // [1, 2, 3, 4, 5, 6]
```

**[⬆ Volver al índice](#índice)**

### **12.6 Valores Falsy**
Los **valores falsy** son aquellos que se evalúan como `false` en un contexto booleano. Los valores falsy en JavaScript incluyen:
- `false`
- `0`
- `""` (string vacío)
- `null`
- `undefined`
- `NaN`

Ejemplo:
```js
if (!0) {
  console.log("Esto es falsy");
}
```

**[⬆ Volver al índice](#índice)**

### **12.7 Operador de Fusión Nula (`??`)**
El **operador de fusión nula** (`??`) se usa para proporcionar un valor por defecto solo si el operando izquierdo es `null` o `undefined`. Es diferente del operador OR (`||`), ya que este considera otros valores falsy como `0` o `""`.

Ejemplo:
```js
let valor = null;
let resultado = valor ?? "Valor por defecto";
console.log(resultado); // "Valor por defecto"

let valor2 = 0;
let resultado2 = valor2 ?? "Valor por defecto";
console.log(resultado2); // 0 (ya que 0 no es null ni undefined)
```

**[⬆ Volver al índice](#índice)**