# Expresiones Regulares en JavaScript

En JavaScript, las **expresiones regulares** (RegExp) son patrones utilizados para buscar y manipular cadenas de texto. Estas expresiones utilizan **caracteres especiales** o **metacaracteres** que tienen significados específicos y permiten crear patrones de búsqueda complejos. A continuación, se detallan los principales tipos de estos caracteres especiales y cómo se usan, especialmente en métodos como `replace()`.

---

## 1. Clases de caracteres (Character Classes)

- **`[...]`**: Coincide con cualquier carácter dentro de los corchetes.
  - **Ejemplo**: `/[aeiou]/` coincide con cualquier vocal en minúscula.
- **`[^...]`**: Coincide con cualquier carácter que **no** esté dentro de los corchetes.
  - **Ejemplo**: `/[^0-9]/` coincide con cualquier carácter que no sea un dígito.
- **Rangos**: Puedes especificar rangos dentro de los corchetes.
  - **Ejemplo**: `/[a-z]/` coincide con cualquier letra minúscula entre 'a' y 'z'.

## 2. Metacaracteres de clase predefinidos

- **`.`**: Coincide con **cualquier carácter** excepto el salto de línea.
  - **Ejemplo**: `/a./` coincide con 'a' seguido de cualquier carácter.
- **`\d`**: Coincide con cualquier **dígito** (equivalente a `[0-9]`).
  - **Ejemplo**: `/\d+/` coincide con uno o más dígitos consecutivos.
- **`\D`**: Coincide con cualquier **no dígito** (equivalente a `[^0-9]`).
- **`\w`**: Coincide con cualquier carácter **alfanumérico** o guion bajo (equivalente a `[A-Za-z0-9_]`).
- **`\W`**: Coincide con cualquier carácter que **no** sea alfanumérico ni guion bajo.
- **`\s`**: Coincide con cualquier **espacio en blanco** (espacio, tabulación, salto de línea).
- **`\S`**: Coincide con cualquier carácter que **no** sea un espacio en blanco.
- **`\b`**: Coincide con una **frontera de palabra** (inicio o fin de una palabra).
  - **Ejemplo**: `/\bcat\b/` coincide con 'cat' como palabra completa.
- **`\B`**: Coincide donde **no** hay una frontera de palabra.

## 3. Anclas

- **`^`**: Coincide con el **inicio** de la cadena o línea (si se usa el modificador `m`).
  - **Ejemplo**: `/^Hola/` coincide si la cadena comienza con 'Hola'.
  - [no confundir con el otro ^ que va dentro de \[\]]
- **`$`**: Coincide con el **final** de la cadena o línea.
  - **Ejemplo**: `/adiós$/` coincide si la cadena termina con 'adiós'.

## 4. Cuantificadores

- **`*`**: Coincide con el elemento anterior **cero o más veces**.
	   **Ejemplo**: `/ho*/` coincide con 'h', 'ho', 'hoo', etc.
  
- **`+`**: Coincide con el elemento anterior **una o más veces**.
	   **Ejemplo**: `/ho+/` coincide con 'ho', 'hoo', pero no con 'h'.
  
- **`?`**: Coincide con el elemento anterior **cero o una vez**.
	   **Ejemplo**: `/colou?r/` coincide con 'color' y 'colour'.
  
- **`{n}`**: Coincide con exactamente **n** repeticiones del elemento anterior.
	   **Ejemplo**: `/\d{3}/` coincide con exactamente tres dígitos.
  
- **`{n,}`**: Coincide con **n o más** repeticiones.
	  -**Ejemplo**: `/\d{2,}/` coincide con dos o más dígitos.
  
- **`{n,m}`**: Coincide con al menos **n** y como máximo **m** repeticiones.
	   **Ejemplo**: `/\d{2,4}/` coincide con dos, tres o cuatro dígitos.

## 5. Grupos y referencias

- **`(...)`**: Define un **grupo de captura**.
  - **Ejemplo**: `/(abc)/` captura 'abc' para referencias posteriores.
- **`(?:...)`**: Define un **grupo sin captura** (no almacena el resultado).
- **`\n`**: Referencia al **n-ésimo grupo capturado**.
  - **Ejemplo**: `/(.)\1/` coincide con caracteres duplicados (ej., 'aa').
- **Alternación**: **`x|y`** coincide con **'x' o 'y'**.
  - **Ejemplo**: `/rojo|azul/` coincide con 'rojo' o 'azul'.

## 6. Lookahead y Lookbehind (Avances y retrocesos)

- **`(?=...)`**: **Lookahead positivo**; coincide si el patrón a la derecha existe.
  - **Ejemplo**: `/\d+(?= euros)/` coincide con dígitos seguidos de ' euros', sin incluir ' euros'.
- **`(?!...)`**: **Lookahead negativo**; coincide si el patrón a la derecha no existe.
- **`(?<=...)`**: **Lookbehind positivo**; coincide si el patrón a la izquierda existe.
- **`(?<!...)`**: **Lookbehind negativo**; coincide si el patrón a la izquierda no existe.

> **Nota**: Los lookbehind están disponibles a partir de ECMAScript 2018.

## 7. Caracteres de escape

- **`\`**: Se utiliza para **escapar** metacaracteres y tratarlos como literales.
  - **Ejemplo**: `/\./` coincide con un punto literal '.'.

## 8. Modificadores (Flags)

- **`g`**: Búsqueda **global** (no se detiene en la primera coincidencia).
- **`i`**: Búsqueda **insensible a mayúsculas/minúsculas**.
- **`m`**: Búsqueda en **múltiples líneas**.
- **`u`**: Trata el patrón como una secuencia de **puntos de código Unicode**.
- **`y`**: Búsqueda **"sticky"**; coincide desde la posición actual en la cadena.

---

## Uso en el método `replace()`

El método `replace()` puede utilizar expresiones regulares para encontrar y reemplazar patrones en una cadena. Puedes utilizar grupos de captura para reutilizar partes de la cadena coincidente en el reemplazo.

**Ejemplo: Formatear una fecha**

```javascript
let fecha = "La fecha es 2023-10-04";
let nuevaFecha = fecha.replace(/(\d{4})-(\d{2})-(\d{2})/, "$3/$2/$1");
console.log(nuevaFecha); // "La fecha es 04/10/2023"
```

En este ejemplo:

- **Patrón**: `/\d{4}-(\d{2})-(\d{2})/`
  - **`(\d{4})`**: Captura el año de cuatro dígitos.
  - **`(\d{2})`**: Captura el mes.
  - **`(\d{2})`**: Captura el día.
- **Reemplazo**: `"$3/$2/$1"`
  - Reordena los grupos capturados para cambiar el formato a `día/mes/año`.

**Ejemplo: Eliminar espacios extra**

```javascript
let texto = "Esto    tiene   espacios    extra.";
let textoSinEspacios = texto.replace(/\s+/g, " ");
console.log(textoSinEspacios); // "Esto tiene espacios extra."
```

- **Patrón**: `/\s+/g`
  - **`\s+`**: Coincide con uno o más espacios en blanco consecutivos.
  - **`g`**: Modificador global para reemplazar todas las ocurrencias.

---

## Resumen de los principales metacaracteres

- **Clases de caracteres**: `[ ]`, `[^ ]`, `[a-z]`
- **Metacaracteres predefinidos**: `.`, `\d`, `\D`, `\w`, `\W`, `\s`, `\S`, `\b`, `\B`
- **Anclas**: `^`, `$`
- **Cuantificadores**: `*`, `+`, `?`, `{n}`, `{n,}`, `{n,m}`
- **Grupos y referencias**: `(...)`, `(?:...)`, `\n`, `x|y`
- **Lookahead y Lookbehind**: `(?=...)`, `(?!...)`, `(?<=...)`, `(?<!...)`
- **Escape**: `\`

Al combinar estos metacaracteres y constructos, puedes crear expresiones regulares potentes para buscar y manipular cadenas de texto de manera eficiente en JavaScript.