# 3. Expresiones Lambda en Java 8

## 3.1 Introducción a Lambdas
- **Definición de Expresiones Lambda**: Una expresión lambda puede entenderse como una especie de **función anónima**: no tiene nombre, pero tiene una lista de **parámetros**, un **cuerpo**, un **tipo de devolución**, y posiblemente una lista de **excepciones** que se pueden lanzar. Simplifica el código al reducir la necesidad de clases anónimas y permite usar un enfoque más **funcional** en Java.
  - Ejemplo básico:
  
  ```java
  (int a, int b) -> a + b;
  ```
  Esta lambda toma dos enteros y devuelve su suma.

- **Comparación entre Lambdas y Clases Anónimas**:
  - Antes de Java 8, para pasar un comportamiento como parámetro se utilizaban **clases anónimas**, lo cual requería escribir más código.
  - Las **expresiones lambda** permiten escribir ese mismo comportamiento de manera más clara y concisa.
  
  ```java
  // Sin lambdas - Clase anónima
  Comparator<Dish> cmpClaseAnonima = new Comparator<Dish>() {
      @Override
      public int compare(Dish dish1, Dish dish2) {
          return Integer.compare(dish1.getCalories(), dish2.getCalories());
      }
  };
  Collections.sort(lowCaloricDishes, cmpClaseAnonima);

  // Con lambda
  Comparator<Dish> cmpLambda = (dish1, dish2) -> Integer.compare(dish1.getCalories(), dish2.getCalories());
  Collections.sort(lowCaloricDishes, cmpLambda);
  ```
  Como se puede observar, la lambda reduce el código considerablemente.

- **Interfaces Funcionales**: Las expresiones lambda solo funcionan cuando se espera una **interfaz funcional**. Una **interfaz funcional** es una interfaz que declara exactamente un único método abstracto.
  - Ejemplo: `Runnable`, `Callable`, `Comparator` son todas interfaces funcionales.
  - Podemos utilizar la anotación `@FunctionalInterface` para asegurarnos de que una interfaz cumple con esta restricción.

  ```java
  @FunctionalInterface
  interface Operacion {
      int realizar(int a, int b);
  }
  ```

- **Uso de Lambdas con Interfaces Funcionales**: Las lambdas se usan únicamente donde se espera una interfaz funcional.
  
  ```java
  List<String> nombres = Arrays.asList("Juan", "Pedro", "Maria");
  nombres.forEach(nombre -> System.out.println(nombre));
  ```
  En este ejemplo, `forEach` espera una interfaz funcional `Consumer`, y podemos pasar una lambda que recibe un `nombre` y lo imprime.

## 3.2 Reemplazo de Lambdas por Referencias a Métodos
- Las **referencias a métodos** son una forma más concisa de escribir una expresión lambda que llama a un método ya existente. Son especialmente útiles cuando la lambda solo llama a un método específico.

### 3.2.1 Reemplazo por Método Estático
- Se puede reemplazar una lambda que llama a un **método estático** con una referencia directa al método.
  
  ```java
  // Lambda
  Consumer<String> imprimir = mensaje -> System.out.println(mensaje);
  
  // Referencia a método estático
  Consumer<String> imprimirRef = System.out::println;
  ```
  Aquí estamos reemplazando `mensaje -> System.out.println(mensaje)` por la referencia al método `System.out::println`.

### 3.2.2 Reemplazo por Método de Instancia de un Objeto Arbitrario
- Si una lambda se refiere a un método de instancia de un **objeto arbitrario**, se puede utilizar una referencia a método de instancia.
  
  ```java
  // Lambda
  Function<String, Integer> parsear = s -> Integer.parseInt(s);
  
  // Referencia a método de instancia
  Function<String, Integer> parsearRef = Integer::parseInt;
  ```
  En este caso, `s -> Integer.parseInt(s)` se puede reemplazar por `Integer::parseInt`.

### 3.2.3 Reemplazo por Método de Instancia de un Objeto Particular
- Cuando la lambda llama a un método de **una instancia específica**, se puede reemplazar con una referencia al método de esa instancia.
  
  ```java
  // Instancia particular
  String mensaje = "Hola Mundo";
  
  // Lambda
  Supplier<String> proveedor = () -> mensaje.toUpperCase();
  
  // Referencia a método de instancia
  Supplier<String> proveedorRef = mensaje::toUpperCase;
  ```
  En este caso, `() -> mensaje.toUpperCase()` se puede reemplazar con `mensaje::toUpperCase`. Aquí no se necesitan parámetros porque `toUpperCase()` no toma argumentos; simplemente utiliza el objeto `mensaje` y devuelve la versión en mayúsculas.

### 3.2.4 Resumen de Transformaciones de Lambdas a Referencias a Métodos
- **Método Estático**: `(args) -> Clase.metodo(args)` se convierte en `Clase::metodo`.
- **Método de Instancia de un Objeto Arbitrario**: `(obj) -> obj.metodo()` se convierte en `Clase::metodo`.
- **Método de Instancia de un Objeto Particular**: `() -> instancia.metodo()` se convierte en `instancia::metodo`.

### 3.2.5 Tabla de Ejemplos de Transformaciones a Referencias a Métodos
| Lambda                                    | Referencia a Método         | Interfaz Funcional        |
|-------------------------------------------|-----------------------------|---------------------------|
| `(x) -> Math.abs(x)`                      | `Math::abs`                 | `Function<Integer, Integer>` |
| `s -> s.toLowerCase()`                    | `String::toLowerCase`       | `Function<String, String>` |
| `(a, b) -> a.compareTo(b)`                | `String::compareTo`         | `BiFunction<String, String, Integer>` |

## 3.3 Closure y Uso de Variables Locales
- **Closure**: Una **closure** es una función que recuerda el entorno donde fue creada, incluso si se utiliza fuera de ese contexto. En Java, las lambdas se comportan como closures, ya que pueden acceder a variables externas definidas en su contexto.

- **Restricción en Lambdas**: En Java, las lambdas **no pueden modificar** las variables locales que se definen fuera de la lambda. Esto se debe a que estas variables se tratan como **finales efectivas**, es decir, no pueden ser cambiadas una vez que la lambda las utiliza.
  - Esto tiene que ver con la forma en que Java maneja las variables en entornos **multi-hilo**. Si se permitiera modificar variables locales dentro de una lambda, podría resultar en comportamientos no deseados cuando múltiples hilos intenten acceder o modificar esas variables al mismo tiempo.

- **Ejemplo de Closure y Variables Locales**:
  
  ```java
  public class EjemploClosure {
      public static void main(String[] args) {
          String saludo = "Hola";  // Variable externa
          
          Runnable r = () -> {
              System.out.println(saludo);  // Uso de la variable externa dentro de la lambda
          };
          
          r.run();
      }
  }
  ```
  En este ejemplo, la variable `saludo` es una variable local del método `main` y es utilizada dentro de la lambda. Aunque no esté marcada como `final`, Java la trata como **final efectiva**, lo cual significa que no se puede modificar después de ser usada en la lambda. Por ejemplo, si intentáramos hacer `saludo = "Hola de nuevo";` después de la definición de la lambda, obtendríamos un error de compilación.

## 3.3.1 Repaso de la Memoria en Java: Stack vs Heap
- **Stack y Heap**:
  - **Stack**: Es el área de memoria donde se almacenan las **variables locales** y las llamadas a métodos. Cada hilo tiene su propio stack, lo cual asegura que las variables locales no se compartan entre hilos.
  - **Heap**: Es el área de memoria donde se almacenan los **objetos** creados con `new`. Los objetos en el heap son compartidos entre todos los hilos, lo cual permite que varios hilos trabajen con el mismo objeto.

- **Ejemplo Visual**:
  
  ```java
  public class EjemploMemoria {
      public static void main(String[] args) {
          int x = 10;  // `x` está en el stack
          Persona persona = new Persona("Juan");  // `persona` está en el heap
      }
  }
  
  class Persona {
      String nombre;
      Persona(String nombre) {
          this.nombre = nombre;
      }
  }
  ```
  En este ejemplo, la variable `x` se almacena en el **stack**, mientras que el objeto `persona` se almacena en el **heap**. Las lambdas pueden acceder a `persona` sin problemas, pero `x` no puede ser modificada una vez que es utilizada por la lambda.