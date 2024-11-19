# valueOf  `Tipo.valueOf(variable)` 
Ejemplo
`               out.write(String.valueOf(num));`
>[!la primera en mayuscula! llamamos a la clase no al primitivo]
> `Double.valueOf(coso)`
# (Parentesis) `(tipo) loquecasteamos`
Este es el casteo clásico pero casi nunca funciona.

# String a int `Integer.parseInt(cadena)`
Para convertir un `String` a un `int`, utilizamos el método `parseInt` de la clase `Integer`.

```java
String numeroStr = "123";
int numero = Integer.parseInt(numeroStr);
```

# String a double `Double.parseDouble(cadena)`
Si necesitas convertir un `String` a `double`, puedes usar el método `parseDouble` de la clase `Double`.

```java
String decimalStr = "3.14159";
double pi = Double.parseDouble(decimalStr);
```

# int/double a String `String.valueOf(numero)`
Convertir un `int` o `double` a `String` es sencillo con el método `String.valueOf`, aunque concatenar el número con una cadena vacía también funciona.

```java
int numero = 321;
String numeroStr = String.valueOf(numero);
// O puedes usar: numero + ""
String numeroStr =""+numero;
```

# Arrays a  Strings `Arrays.toString(elArray)`
Para convertir un array de `int` a un String, puedes usar `Arrays.toString(array)`.

```java
int[] numeros = {1, 2, 3, 4, 5};
String arrayComoString = Arrays.toString(numeros);
```


# tipo a String `Tipo.toString()`
Sirve para long, boolean
- `Long.toString(numeroGrande)`
-  `Boolean.toString(decision)`
- `Character.toString(letra)`
# char a String y viceversa 
- `Character.toString(letra)`
- `letra.charAt(0)`

```java
char letra = 'a';
String letraComoString = Character.toString(letra);
char stringALetra = letraComoString.charAt(0); // Siempre asegúrate de que el String no esté vacío
```

# String a char [] `cad.toCharArray()`
`char letras [] = frase.toCharArray();`
# Parsear FECHAS! `LocalDate.parse(cadenaFecha)`

```java
String fechaComoString = "2023-05-10";
//de String a LocalDate
LocalDate fecha = LocalDate.parse(fechaComoString);
//de LocalDate a String
String fechaComoString = fecha.toString();

```

