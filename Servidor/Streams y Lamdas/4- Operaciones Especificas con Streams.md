## 4.1 filter
- **Uso de filter**: `filter()` se usa para obtener elementos de un stream que cumplen una condición específica (un **predicado**).
  - Ejemplo:
  
  ```java
  List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6);
  List<Integer> pares = numeros.stream()
                               .filter(n -> n % 2 == 0)
                               .collect(Collectors.toList());
  System.out.println(pares);  // [2, 4, 6]
  ```
  - **Comparación con bucles tradicionales**: En un bucle `for`, se necesitaría verificar cada elemento manualmente con un `if`. Con `filter()`, podemos hacerlo en una sola línea de forma más clara.

  - **Ejemplo adicional**: Filtrando cadenas de texto.
  
  ```java
  List<String> nombres = Arrays.asList("Ana", "Juan", "Pedro", "Lucia");
  List<String> nombresConA = nombres.stream()
                                    .filter(nombre -> nombre.contains("a"))
                                    .collect(Collectors.toList());
  System.out.println(nombresConA);  // [Ana, Juan, Lucia]
  ```

## 4.2 sorted
- **Uso de sorted**: `sorted()` se usa para ordenar los elementos de un stream.
  - Ejemplo de uso con un comparador:
  
  ```java
  List<String> nombres = Arrays.asList("Juan", "Ana", "Pedro", "Lucia");
  List<String> nombresOrdenados = nombres.stream()
                                         .sorted()  // Orden natural
                                         .collect(Collectors.toList());
  System.out.println(nombresOrdenados);  // [Ana, Juan, Lucia, Pedro]
  
  List<String> nombresPorLongitud = nombres.stream()
                                           .sorted(Comparator.comparing(String::length))  // Comparador por longitud
                                           .collect(Collectors.toList());
  System.out.println(nombresPorLongitud);  // [Ana, Juan, Pedro, Lucia]
  ```
  - **Ejemplo adicional**: Ordenando números en orden descendente.
  
  ```java
  List<Integer> numeros = Arrays.asList(5, 2, 8, 1, 4);
  List<Integer> numerosOrdenadosDesc = numeros.stream()
                                              .sorted(Comparator.reverseOrder())
                                              .collect(Collectors.toList());
  System.out.println(numerosOrdenadosDesc);  // [8, 5, 4, 2, 1]
  ```

## 4.3 distinct
- **Uso de distinct**: `distinct()` se usa para eliminar duplicados en un stream.
  - Ejemplo:
  
  ```java
  List<Integer> numeros = Arrays.asList(1, 2, 2, 3, 4, 4, 5);
  List<Integer> unicos = numeros.stream()
                                .distinct()
                                .collect(Collectors.toList());
  System.out.println(unicos);  // [1, 2, 3, 4, 5]
  ```
  - **Ejemplo adicional**: Eliminando cadenas duplicadas.
  
  ```java
  List<String> palabras = Arrays.asList("hola", "mundo", "hola", "java");
  List<String> palabrasUnicas = palabras.stream()
                                        .distinct()
                                        .collect(Collectors.toList());
  System.out.println(palabrasUnicas);  // [hola, mundo, java]
  ```

## 4.4 takeWhile (Java 9)
- **Uso de takeWhile**: `takeWhile()` se usa para tomar elementos de un stream hasta que un predicado deje de cumplirse.
  - Ejemplo:
  
  ```java
  List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6);
  List<Integer> menoresDeCuatro = numeros.stream()
                                         .takeWhile(n -> n < 4)
                                         .collect(Collectors.toList());
  System.out.println(menoresDeCuatro);  // [1, 2, 3]
  ```
  - **Ejemplo adicional**: Usando `takeWhile` con cadenas.
  
  ```java
  List<String> nombres = Arrays.asList("Ana", "Carlos", "Beatriz", "David");
  List<String> hastaC = nombres.stream()
                               .takeWhile(nombre -> nombre.compareTo("C") < 0)
                               .collect(Collectors.toList());
  System.out.println(hastaC);  // [Ana]
  ```

## 4.5 dropWhile (Java 9)
- **Uso de dropWhile**: `dropWhile()` se usa para descartar elementos de un stream hasta que el predicado deje de cumplirse.
  - Ejemplo:
  
  ```java
  List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6);
  List<Integer> desdeCuatro = numeros.stream()
                                     .dropWhile(n -> n < 4)
                                     .collect(Collectors.toList());
  System.out.println(desdeCuatro);  // [4, 5, 6]
  ```
  - **Ejemplo adicional**: Usando `dropWhile` con cadenas.
  
  ```java
  List<String> nombres = Arrays.asList("Ana", "Carlos", "Beatriz", "David");
  List<String> desdeC = nombres.stream()
                               .dropWhile(nombre -> nombre.compareTo("C") < 0)
                               .collect(Collectors.toList());
  System.out.println(desdeC);  // [Carlos, Beatriz, David]
  ```

## 4.6 limit
- **Uso de limit**: `limit()` se usa para obtener un número específico de elementos de un stream.
  - Ejemplo:
  
  ```java
  List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5);
  List<Integer> primerosTres = numeros.stream()
                                      .limit(3)
                                      .collect(Collectors.toList());
  System.out.println(primerosTres);  // [1, 2, 3]
  ```
  - **Ejemplo adicional**: Limitando cadenas.
  
  ```java
  List<String> nombres = Arrays.asList("Ana", "Juan", "Pedro", "Lucia");
  List<String> primerosDos = nombres.stream()
                                    .limit(2)
                                    .collect(Collectors.toList());
  System.out.println(primerosDos);  // [Ana, Juan]
  ```

## 4.7 skip
- **Uso de skip**: `skip()` se usa para descartar un número específico de elementos de un stream.
  - Ejemplo:
  
  ```java
  List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5);
  List<Integer> sinLosPrimerosDos = numeros.stream()
                                           .skip(2)
                                           .collect(Collectors.toList());
  System.out.println(sinLosPrimerosDos);  // [3, 4, 5]
  ```
  - **Ejemplo adicional**: Saltando cadenas.
  
  ```java
  List<String> nombres = Arrays.asList("Ana", "Juan", "Pedro", "Lucia");
  List<String> sinLosPrimerosTres = nombres.stream()
                                           .skip(3)
                                           .collect(Collectors.toList());
  System.out.println(sinLosPrimerosTres);  // [Lucia]
  ```

## 4.8 map
- **Uso de map**: `map()` se usa para transformar elementos de un stream.
  - Ejemplo de transformación de cadenas:
  
  ```java
  List<String> nombres = Arrays.asList("Juan", "Ana", "Pedro");
  List<String> nombresMayusculas = nombres.stream()
                                          .map(String::toUpperCase)
                                          .collect(Collectors.toList());
  System.out.println(nombresMayusculas);  // [JUAN, ANA, PEDRO]
  ```
  - Ejemplo de transformación de objetos:
  
  ```java
  List<Integer> numeros = Arrays.asList(1, 2, 3);
  List<Integer> cuadrados = numeros.stream()
                                   .map(n -> n * n)
                                   .collect(Collectors.toList());
  System.out.println(cuadrados);  // [1, 4, 9]
  ```
  - **Ejemplo adicional**: Transformando objetos complejos.
  
  ```java
  class Persona {
      String nombre;
      Persona(String nombre) { this.nombre = nombre; }
  }
  
  List<Persona> personas = Arrays.asList(new Persona("Juan"), new Persona("Ana"), new Persona("Pedro"));
  List<String> nombresPersonas = personas.stream()
                                         .map(persona -> persona.nombre)
                                         .collect(Collectors.toList());
  System.out.println(nombresPersonas);  // [Juan, Ana, Pedro]
  ```

## 4.9 flatMap
- **Uso de flatMap**: `flatMap()` se usa para **aplanar** estructuras complejas, como listas de listas, en un único stream.
  - Comparación con `map()`: `map()` transforma cada elemento, pero mantiene la estructura, mientras que `flatMap()` aplanará el resultado.
  - Ejemplo con arrays:
  
  ```java
  List<List<String>> listas = Arrays.asList(
      Arrays.asList("A", "B"),
      Arrays.asList("C", "D"),
      Arrays.asList("E", "F")
  );
  List<String> aplanada = listas.stream()
                                .flatMap(List::stream)
                                .collect(Collectors.toList());
  System.out.println(aplanada);  // [A, B, C, D, E, F]
  ```
  - **Ejemplo adicional**: Aplanando listas de números.
  
  ```java
  List<List<Integer>> numeros = Arrays.asList(
      Arrays.asList(1, 2),
      Arrays.asList(3, 4),
      Arrays.asList(5, 6)
  );
  List<Integer> numerosAplanados = numeros.stream()
                                          .flatMap(List::stream)
                                          .collect(Collectors.toList());
  System.out.println(numerosAplanados);  // [1, 2, 3, 4, 5, 6]
  ```

## 4.10 allMatch, anyMatch, noneMatch
- **Uso de allMatch, anyMatch, noneMatch** para comprobar condiciones en los elementos de un stream.
  - **allMatch()**: Comprueba si **todos** los elementos cumplen un predicado.
  
  ```java
  boolean todosPares = numeros.stream().allMatch(n -> n % 2 == 0);
  System.out.println(todosPares);  // false
  ```
  - **anyMatch()**: Comprueba si **algún** elemento cumple un predicado.
  
  ```java
  boolean algunPar = numeros.stream().anyMatch(n -> n % 2 == 0);
  System.out.println(algunPar);  // true
  ```
  - **noneMatch()**: Comprueba si **ningún** elemento cumple un predicado.
  
  ```java
  boolean ningunMayorQueDiez = numeros.stream().noneMatch(n -> n > 10);
  System.out.println(ningunMayorQueDiez);  // true
  ```
  - **Ejemplo adicional**: Usando `anyMatch()` con cadenas.
  
  ```java
  List<String> nombres = Arrays.asList("Ana", "Pedro", "Juan");
  boolean hayPedro = nombres.stream().anyMatch(nombre -> nombre.equals("Pedro"));
  System.out.println(hayPedro);  // true
  ```

## 4.11 findAny, findFirst
- **Uso de findAny y findFirst** para obtener un elemento opcional de un stream.
  - **findFirst()**: Obtiene el **primer** elemento del stream.
  
  ```java
  Optional<Integer> primero = numeros.stream().findFirst();
  primero.ifPresent(System.out::println);  // 1
  ```
  - **findAny()**: Obtiene **cualquier** elemento del stream (especialmente útil en streams paralelos).
  
  ```java
  Optional<Integer> cualquiera = numeros.stream().findAny();
  cualquiera.ifPresent(System.out::println);  // 1 (u otro, dependiendo del caso)
  ```
  - Ambos devuelven un `Optional<T>`, lo cual es útil para manejar la posible ausencia de valor de una forma segura.
  - **Ejemplo adicional**: `findAny()` en un stream paralelo.
  
  ```java
  Optional<Integer> elementoParalelo = numeros.parallelStream().findAny();
  elementoParalelo.ifPresent(System.out::println);  // Resultado no predecible
  ```

## 4.12 reduce
- **Uso de reduce**: `reduce()` se usa para combinar los elementos de un stream en un único resultado.

### 4.12.1 reduce con Valor Inicial
- **Reduce con valor inicial**: Se usa un valor inicial que se acumula con cada elemento del stream.
  - Ejemplo de suma:
  
  ```java
  int suma = numeros.stream().reduce(0, (a, b) -> a + b);
  System.out.println(suma);  // 21
  ```
  - Ejemplo de multiplicación:
  
  ```java
  int producto = numeros.stream().reduce(1, (a, b) -> a * b);
  System.out.println(producto);  // 720
  ```
  - **Ejemplo adicional**: Concatenando cadenas.
  
  ```java
  List<String> palabras = Arrays.asList("Hola", "Mundo", "Java");
  String frase = palabras.stream().reduce("", (a, b) -> a + " " + b).trim();
  System.out.println(frase);  // Hola Mundo Java
  ```

### 4.12.2 reduce sin Valor Inicial
- **Reduce sin valor inicial**: En este caso, `reduce()` devuelve un `Optional<T>` para manejar la posibilidad de un stream vacío.
  
  ```java
  Optional<Integer> suma = numeros.stream().reduce((a, b) -> a + b);
  suma.ifPresent(System.out::println);  // 21
  ```
  - **Ejemplo adicional**: Encontrando el máximo valor sin valor inicial.
  
  ```java
  Optional<Integer> maximo = numeros.stream().reduce(Integer::max);
  maximo.ifPresent(System.out::println);  // 6
  ```

### 4.12.3 reduce a Max y Min
- **Uso de reduce para encontrar el máximo y mínimo**:
  - Ejemplo de máximo:
  
  ```java
  Optional<Integer> max = numeros.stream().reduce(Integer::max);
  max.ifPresent(System.out::println);  // 6
  ```
  - Ejemplo de mínimo:
  
  ```java
  Optional<Integer> min = numeros.stream().reduce(Integer::min);
  min.ifPresent(System.out::println);  // 1
  ```
  - **Ejemplo adicional**: Encontrando la cadena más larga.
  
  ```java
  List<String> palabras = Arrays.asList("Hola", "Mundo", "Java");
  Optional<String> masLarga = palabras.stream().reduce((a, b) -> a.length() > b.length() ? a : b);
  masLarga.ifPresent(System.out::println);  // Mundo
  ```