# String a char [] `toCharArray()`

`char letras [] = frase.toCharArray();`
# `char` 'c'

se pueden usar directamente a int en su valor numerico y viceversa y mezclado
ej: 'a'+1 = 'b'

`'a'-'A'` repesenta la distancia entre las mayusculas y las minusculas.
 *a=65  A=97; la diferencia es 32:*
ej: 'h' + 'a'-'A' = 'H'

## Unicode
se representa con \\u y cuatro digitos (hexadecimal) o code point, decimal (97)
ej: 'a' = 97 = '\\u0061' 

## clasificación y conversión de caracteres
Segun el tipo de caracter podemos usar la expresion booleana `boolean isTipo(char c)`  para identificarlo

- Dígitos  0, 1, 2, 3,... `isDigit(c)` `isLetterorDigit(c)`
- Letras a b c d d e... ``idLetter(c) `isLetterorDigit(c)`
`isLowerCase(c)`
`isUpperCase(c)`
`char toLowerCase(c)`
``char to UpperCase(c)
- #### **Caracteres en blanco:** `isWhiteSpace(c)`
	-  Espacio (`U+0020`) `isSpaceChar(c)`
	- Tabulador horizontal (`U+0009`)
	- Nueva línea (`U+000A`)
	- Retorno de carro (`U+000D`)
	- Y otros varios espacios definidos por Unicode que cubren diferentes anchos y usos
- Otros caracteres: signos de puntuacion, matemáticos, etc...
## secuencias de escape:

	- \\b Borrado a la izquierda
	- \\n  Nueva línea
	- \\r Retorno de carro
	- \\t Tabulador
	- \\f Nueva Página
	- \\' Comilla simple
	- \\" Comilla doble
	- \\\\ 

ej: `char c = '\''`; comilla simple


# String

- literal cadena "lo que quieras incluso incluyendo caracteres con secunecia de escape \\u2661"
- se concatena con + "bla"+" bla"
- posicion de un caracter en la cadena con `.charAt(0)`
- la longitud de una cadena se calcula con `.length()`
## Subcadenas y manipulación de la cadena

- `cad1.substring(28)` subcadena DESDE el caracter 28
- `cad1.substring(15,28)` desde el 15 al 27 (uno menos al que pongas)
- `cad1.strip()` elimina los caracteres blancos del principio y el final.
-  `cad1.stripLeading()` elimina los caracteres blancos del principio.
-  `cad1.stripTrailing()` elimina los caracteres blancos del final.

- pasar a minusculas `.toLowerCase()`
- pasar a mayusculas `.toUpperCase()`

- `cad1.replace('a','\\u2764')`devuelve una copia de la cadena cambiando un caracter `'a'` por otro `❤️` . vale con char y con cadenas/charSequence.
- `String [] palabras frase.split(" ")` devuelve las subcadenas resultantes eliminiando el caracter, en este caso un espacio.
### Comparación `cad1.equals(cad2)` y `regionMatches`
	
- `cad1.equalsIgnoreCase(cad2)` ignora mayusculas y minúsculas
-  `cad.regionMatches(inicioCad1 3, cad2,iniciocad2 10,longitud 5)`solo un troco.
- `cad.regionMatches(true, inicioCad1 3, cad2,iniciocad2 10,longitud 5)`igual pero si es `true` ignora Mayusculas y minusculas

- `cad2.compareTo(cad1)`:
	- 0 son iguales
	- +0 lo del parentesis va antes `(cad1)
	- -0 lo del parentesis va después `(cad2)`
	
## conversiones a String `String.valueOf(valor)`
>[!To String] @Override toString
>Realmente valueOf, llama a toString, que si lo tenemos sobrecargado en una clase, tambien nos valdria para llamar a su representacion en cadena. 

- `cad = String.valueOf(1234); /equivale a/ cad = "1234"`
- `cad = String.valueOf(-12.34); /equivale a/ cad = "-12.34"`
- `cad = String.valueOf('x'); /equivale a/ cad = "x"`
- `cad = String.valueOf(false); /equivale a/ cad = "false"`

## Busqueda

- `int indexOf( c)` busca la primera ocurrencia del caracter `c`, se puede usar con cadenas, nos devuelve el primer caracter de la cadena, si no, lo encuentra devuelve un -1. *`cad.indexOf("bla")`*
- `int indexOf(c, desde inicio)// cad.indexOf("pepe", 4)` empieza en 4 y busca pepe. 
- `int lastIndexOf(c)` devuelve la ULTIMA ocurrencia de c y si no -1;
- `int lastIndexOf(cad, desde inicio)` desde el final empezando por inicio hacia el inicio. 

## Comprobaciones

- Boolean `cad1.isEmpty()` true, vacia. False tiene algo.
- Boolean `cad1.contains("caca")` true, hay caca. False no hay caca.
- Boolean `cuento.startsWith("Erase")` empieza por
- Boolean `cuento.endsWith("perdices"` acaba por 






