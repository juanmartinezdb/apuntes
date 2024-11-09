## 5.1 Operación collect
- **Introducción a collect**: `collect()` es una operación terminal en los streams que se usa para realizar una **reducción mutable**, es decir, para acumular los elementos de un stream en una estructura de datos mutable, como una lista, un conjunto o un mapa. Esto se hace mediante el uso de la clase `Collectors` que ofrece métodos útiles para las operaciones de agrupación y reducción.
  - Ejemplo:
  
  ```java
  List<String> nombres = Arrays.asList("Juan", "Ana", "Pedro");
  List<String> nombresLista = nombres.stream().collect(Collectors.toList());
  System.out.println(nombresLista);  // [Juan, Ana, Pedro]
  ```

## 5.2 Ejemplos con collect
### 5.2.1 maxBy y minBy
- **Uso de collect con maxBy y minBy** para encontrar el valor máximo o mínimo en un stream.
  - Ejemplo con `maxBy`:
  
  ```java
  List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6);
  Optional<Integer> maximo = numeros.stream().collect(Collectors.maxBy(Integer::compareTo));
  maximo.ifPresent(System.out::println);  // 6
  ```
  - Ejemplo con `minBy`:
  
  ```java
  Optional<Integer> minimo = numeros.stream().collect(Collectors.minBy(Integer::compareTo));
  minimo.ifPresent(System.out::println);  // 1
  ```

### 5.2.2 Sumarización con collect
- **summingInt, averagingInt, summarizingInt**: `Collectors` tiene varios métodos para sumarizar datos de una manera eficiente.
  - **summingInt**: Suma los valores de los elementos.
  
  ```java
  int suma = numeros.stream().collect(Collectors.summingInt(Integer::intValue));
  System.out.println(suma);  // 21
  ```
  - **averagingInt**: Calcula el promedio de los valores.
  
  ```java
  double promedio = numeros.stream().collect(Collectors.averagingInt(Integer::intValue));
  System.out.println(promedio);  // 3.5
  ```
  - **summarizingInt**: Devuelve un resumen con información como la suma, el promedio, el mínimo y el máximo.
  
  ```java
  IntSummaryStatistics stats = numeros.stream().collect(Collectors.summarizingInt(Integer::intValue));
  System.out.println(stats);  // IntSummaryStatistics{count=6, sum=21, min=1, average=3.500000, max=6}
  ```

- **collect con joining**: `joining()` se usa para concatenar los elementos de un stream en una sola cadena.
  - Ejemplo:
  
  ```java
  List<String> palabras = Arrays.asList("Hola", "Mundo", "Java");
  String frase = palabras.stream().collect(Collectors.joining(" "));
  System.out.println(frase);  // Hola Mundo Java
  ```

## 5.3 Agrupación de Datos
### 5.3.1 groupingBy con Lambdas
- **groupingBy** se usa para agrupar elementos de un stream según una clave especificada.
  - Ejemplo de agrupar platos por nivel calórico:
  
  ```java
  class Plato {
      String nombre;
      int calorias;
      Plato(String nombre, int calorias) { this.nombre = nombre; this.calorias = calorias; }
  }
  
  List<Plato> platos = Arrays.asList(
      new Plato("Ensalada", 200),
      new Plato("Hamburguesa", 800),
      new Plato("Fruta", 150)
  );
  
  Map<String, List<Plato>> platosPorNivelCalorico = platos.stream()
      .collect(Collectors.groupingBy(plato -> plato.calorias > 500 ? "Alto" : "Bajo"));
  
  System.out.println(platosPorNivelCalorico);
  // {Bajo=[Ensalada, Fruta], Alto=[Hamburguesa]}
  ```

### 5.3.2 Agrupación Multinivel
- **Agrupación multinivel**: Podemos agrupar por varios criterios anidados usando `groupingBy` múltiples veces.
  - Ejemplo de agrupar platos por tipo y nivel calórico:
  
  ```java
  class Plato {
      String tipo;
      String nombre;
      int calorias;
      Plato(String tipo, String nombre, int calorias) { this.tipo = tipo; this.nombre = nombre; this.calorias = calorias; }
  }
  
  List<Plato> platos = Arrays.asList(
      new Plato("Vegetariano", "Ensalada", 200),
      new Plato("No Vegetariano", "Hamburguesa", 800),
      new Plato("Vegetariano", "Fruta", 150),
      new Plato("No Vegetariano", "Pollo", 400)
  );
  
  Map<String, Map<String, List<Plato>>> platosPorTipoYNivelCalorico = platos.stream()
      .collect(Collectors.groupingBy(plato -> plato.tipo,
              Collectors.groupingBy(plato -> plato.calorias > 500 ? "Alto" : "Bajo")));
  
  System.out.println(platosPorTipoYNivelCalorico);
  // {Vegetariano={Bajo=[Ensalada, Fruta]}, No Vegetariano={Alto=[Hamburguesa], Bajo=[Pollo]}}
  ```

### 5.3.3 groupingBy y Sumarización
- **Contar y sumar dentro de grupos**: `groupingBy` se puede combinar con otras operaciones, como contar o sumar elementos dentro de cada grupo.
  - Ejemplo de contar elementos en cada grupo:
  
  ```java
  Map<String, Long> cantidadPorNivelCalorico = platos.stream()
      .collect(Collectors.groupingBy(plato -> plato.calorias > 500 ? "Alto" : "Bajo", Collectors.counting()));
  
  System.out.println(cantidadPorNivelCalorico);
  // {Bajo=3, Alto=1}
  ```
  - Ejemplo de sumar calorías en cada grupo:
  
  ```java
  Map<String, Integer> caloriasPorNivelCalorico = platos.stream()
      .collect(Collectors.groupingBy(plato -> plato.calorias > 500 ? "Alto" : "Bajo", Collectors.summingInt(plato -> plato.calorias)));
  
  System.out.println(caloriasPorNivelCalorico);
  // {Bajo=750, Alto=800}
  ```