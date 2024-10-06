# 1. Conceptos Fundamentales de Java 8

## 1.1 Introducción a Lambdas y Streams
- **Lambdas y Streams**: Java 8 introduce las expresiones lambda y los streams como una forma moderna y concisa de manejar colecciones.
- **Diferencia con I/O Streams**: Los streams de Java 8 permiten el manejo declarativo de datos en colecciones, mientras que los flujos de entrada/salida (I/O Streams) manejan la lectura y escritura de datos entre ficheros y la memoria.

## 1.2 Flujos de Entrada/Salida (I/O Streams)
- **Modelo de E/S**: Similar al de Unix, Java divide el flujo de E/S en flujos de bytes y caracteres.
  - **Clases de E/S**:
    - `InputStream` y `OutputStream`: Manejan datos en forma de bytes, como imágenes o archivos binarios.
    - `Reader` y `Writer`: Manejan datos en forma de caracteres, como archivos de texto. Estos flujos usan **codificación Unicode** para representar los caracteres correctamente.
- **Buffered Streams**: Utiliza `BufferedReader` o `BufferedWriter` para mejorar la eficiencia al leer o escribir grandes volúmenes de datos. Los flujos almacenados en búfer permiten leer y escribir en bloques más grandes, lo que resulta en un rendimiento mejorado.

```java
try (BufferedReader reader = new BufferedReader(new FileReader("archivo.txt"))) {
    String linea;
    while ((linea = reader.readLine()) != null) {
        System.out.println(linea);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```
- **Cierre de Flujos**: Es importante cerrar los flujos (utilizando `try-with-resources`) para liberar los recursos del sistema y evitar problemas de memoria o bloqueos en el acceso a archivos.

# 2. Streams en Java 8

## 2.1 Definición y Uso de Streams
- **Streams**: Permiten manipular colecciones de manera **declarativa**, es decir, describiendo lo que queremos hacer con los datos sin preocuparnos de cómo hacerlo en detalle.
  - **Java 7 vs Java 8**: En Java 7, el manejo de colecciones se hacía principalmente con bucles `for` o `while`, lo que requería escribir más líneas de código y era propenso a errores. En Java 8, los streams permiten escribir operaciones complejas en pocas líneas de código y de forma más comprensible.
  - **parallelStream()**: Los streams también se pueden ejecutar en paralelo con `parallelStream()`, lo cual permite dividir el trabajo en varios núcleos del procesador, aumentando la velocidad en algunos casos.

```java
List<String> nombres = Arrays.asList("Juan", "Pedro", "Maria");
nombres.stream()
      .filter(nombre -> nombre.startsWith("J"))
      .map(String::toUpperCase)
      .forEach(System.out::println);
```

## 2.2 Operaciones con Streams: Intermedias y Terminales
### 2.2.1 Operaciones Intermedias
- **Operaciones Intermedias**: Estas operaciones procesan los elementos del stream y devuelven otro stream. Son **perezosas**, lo que significa que no se ejecutan hasta que se encuentre una operación terminal.
  - `filter()`: Filtra elementos que cumplen una condición específica.
  - `map()`: Transforma cada elemento en otro valor. Por ejemplo, convertir todos los nombres a mayúsculas.
  - `limit()`: Limita el número de elementos del stream.
  - `sorted()`: Ordena los elementos del stream.
  - `distinct()`: Elimina elementos duplicados del stream.
  
```java
List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6);
numeros.stream()
       .filter(n -> n % 2 == 0)  // Filtra los números pares
       .map(n -> n * 2)          // Multiplica cada número por 2
       .forEach(System.out::println);  // 4, 8, 12
```

### 2.2.2 Operaciones Terminales
- **Operaciones Terminales**: Estas operaciones finalizan el procesamiento del stream y devuelven un resultado, como una lista, un valor único o simplemente realizan una acción.
  - `forEach()`: Itera sobre cada elemento y realiza una acción, como imprimirlo.
  - `count()`: Devuelve el número de elementos en el stream.
  - `collect()`: Acumula los elementos en una colección, como una lista o un conjunto.
  - `reduce()`: Combina los elementos del stream en un único valor. Por ejemplo, sumar todos los números.

```java
int suma = numeros.stream().reduce(0, Integer::sum);  // suma = 21
```

## 2.3 Streams Numéricos Primitivos
- **Streams Primitivos**: Existen clases especiales para trabajar con tipos de datos primitivos como `int`, `double` o `long`. Estas clases son `IntStream`, `DoubleStream` y `LongStream`. Usar estas clases evita el **auto-boxing**, que es la conversión automática de un tipo de dato primitivo a su correspondiente clase (por ejemplo, de `int` a `Integer`). Esto mejora el rendimiento al evitar operaciones innecesarias de conversión.

```java
IntStream.range(1, 5).forEach(System.out::println);  // 1, 2, 3, 4
```
- **Métodos de sumarización**: También se pueden usar métodos como `sum()`, `max()`, `min()` para realizar operaciones comunes en los streams numéricos.

## 2.4 Rangos Numéricos
- **Generar Rangos**: Con `IntStream.rangeClosed(1, 5)` se pueden generar números consecutivos de forma fácil. Esto es útil para crear bucles sin necesidad de escribir un bucle explícito.

```java
IntStream.rangeClosed(1, 5).forEach(System.out::println);  // 1, 2, 3, 4, 5
```

## 2.5 Ejemplos Prácticos con Streams
- **Filtrar y Ordenar Transacciones**:

```java
List<Transaction> transacciones = Arrays.asList(
    new Transaction("Trader1", 2021, 100),
    new Transaction("Trader2", 2022, 150)
);
transacciones.stream()
            .filter(t -> t.getYear() == 2021)  // Filtra transacciones del año 2021
            .sorted(Comparator.comparing(Transaction::getValue))  // Ordena por valor
            .forEach(System.out::println);
```

- **Lista de Ciudades de Traders**:

```java
List<String> ciudades = transacciones.stream()
                                     .map(Transaction::getCity)  // Obtiene la ciudad de cada transacción
                                     .distinct()  // Elimina ciudades duplicadas
                                     .collect(Collectors.toList());  // Convierte a lista
```

- **Encontrar y Ordenar Traders en una Ciudad**:

```java
List<Trader> traders = transacciones.stream()
                                    .map(Transaction::getTrader)  // Obtiene el trader de cada transacción
                                    .filter(t -> "Málaga".equals(t.getCity()))  // Filtra traders de Málaga
                                    .distinct()  // Elimina traders duplicados
                                    .sorted(Comparator.comparing(Trader::getName))  // Ordena por nombre
                                    .collect(Collectors.toList());
```

- **Concatenar Nombres de Traders**:

```java
String nombresTraders = traders.stream()
                               .map(Trader::getName)  // Obtiene el nombre de cada trader
                               .collect(Collectors.joining(", "));  // Une los nombres con una coma
```

- **Comprobar si hay Traders en una Ciudad**:

```java
boolean hayTradersEnMalaga = traders.stream()
                                    .anyMatch(t -> "Málaga".equals(t.getCity()));  // Comprueba si hay traders en Málaga
```

- **Transacciones de una Ciudad**:

```java
transacciones.stream()
             .filter(t -> "Málaga".equals(t.getTrader().getCity()))  // Filtra transacciones de traders en Málaga
             .map(Transaction::getValue)  // Obtiene el valor de cada transacción
             .forEach(System.out::println);
```

- **Valor Más Alto y Transacción con Valor Más Bajo**:

```java
Optional<Integer> maxValor = transacciones.stream()
                                          .map(Transaction::getValue)  // Obtiene el valor de cada transacción
                                          .max(Integer::compare);  // Encuentra el valor más alto

Optional<Transaction> minTransaccion = transacciones.stream()
                                                   .min(Comparator.comparing(Transaction::getValue));  // Encuentra la transacción con el valor más bajo
```