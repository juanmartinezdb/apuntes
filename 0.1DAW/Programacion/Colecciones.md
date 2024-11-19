# Intro

![[Pasted image 20240501122155.png]]

importar `java.util.`

Arrays Dinamicos, pueden ser de diferente tipo segun la funcion:
- **Listas** --> Interface `List` el orden puede importar y se pueden repetir 
- **Conjuntos** -->  Inteface `set` no importa el orden y no se pueden repetir
- **Mapas** --> Interface `map` datos identificados por claves y no se pueden repetir.

# Tipos parametrizados o genéricos

Se usan para generalizar la llamada a la función o metodo, por ejemplo la interface `Comparable` usa `Object` en `compareTo(Object ob)` para así se pueda usarla con todo tipo de clases casteandolas:
```java
int compareTo(Object ob) {
	return dni.compareTo(((Cliente)ob).dni);
}
```
### Clases con parámetros genéricos

podemos declarar parametros genericos con la expresion diamante `<patata>` en la clase y luego en la llamada a esta las definiremos de nuevo con el diamante `<Integer>` (pero ojo, tiene que ser una clase o interface no un primitivo por eso `Integer` no `int`)
```java
class claseEjemplo <patata> {
private patata atributoEjemplo; // le atritbuto es generico y lo definiremos al crear los objetos de esta clase. 
}
.....
claseEjemplo<Integer> cosito = new claseEjemplo<>(); //aqui definimos patata como Integer

```
### Interfaces con genéricos
Igual que las clases, además, podemos declarar su tipo generico en el implements ej:
```java
class Compara Nombres implements Comparator<Clientes>{
	public int compare (Cliente o1, Cliente o2) {
		return  o1.nombre.compareTo(o2.nombre);		
	}
}
```
>[!Lambda] 
>Tambien podemos usar una expresion #lambda para resumir la implementacion de una clase anonima y crear un metodo de comparador llamando directamente a al implementacion de `Comparable` de la clase.
```java
Comparator<Cliente> ordenClientes = (c1, c2) -> c1.dni.compareTo.(c2.dni);
```
### Parámetros genéricos limitados
`class Clase<T extends claseLimite>{...}` limita T a objetos de la claseLimite y sus subclases.
	ej: `class Calculadora <T extends Number>{}`

`class Clase<T super claseLimite>{...}` limita T a objetos de la claseLimite y su cadena de superclases hasta `object` que sería la mas genérica hacia arriba.

>[!Interfaces]
>Tambien sirve para interfaces, y seguimos usando **extends** no implements

### Métodos Genéricos
detrás del tipo que nos devuelve el método ponemos nuestros genéricos `<U>` 
```java
static <U> int numeroDeNulos (U[] tabla) {
	int cont =0;
	for (U e : tabla){
		cont++;
	}
	return cont;
}
```

### Comodines '?'
>[!d] MPORTENTE!
>Cuando declaramos una variable con tipo generico, no quiere decir que su tipo generico herede de las clases a las que referencia! 
>`Contenedor<Object> coso = new Contenedor<Integer>`  Esto peta, porque no se aplica herencia, esto se llama **invarianza** porque:
>Integer hereda de Object  --pero-- Contenedor\<Integer\> no hereda de \<Object\>

El `?` junto con la declaracion de parametros limitados sirve para salvar la invarianza usando 
- `? extends Tipo` cualquiera del tipo subtipo
- `? super Tipo`  cualquiera del tipo o de sus supertipo hasta `Object`

coso puede referenciar Integer, Double Float... todos los subtipos de Number en este caso Integer
```java
Contenedor<? extends Number> coso = new Contenedor<Integer>();
```

otroCoso puede ser Integer, number u Object. pero podemos insertar un Inger en otroCoso.
```java
Contenedor<? super Integer> otroCoso = new Contenedor<Number>();
```

### Cosas que NO se pueden hacer con parametros genéricos.
- Los tipos gnéricos nunca pueden ser primitvos.
- No se pueden crear instancias de tipos gneéricos, como `new T()`.
- No se pueden crear tablas de tipo genérico como en `new T[10]`
- No se pueden crear tablas de clases parametrizadas como `new Contenedor<Integer>[5]`
- No se pueden usar excepciones genéricas.

# Métodos de la Interfaz Collection en Java

Para explicar los métodos de la colección, usaremos vinculación dinámica bajo el concepto de herencia para usar las siguiente variables haciendo que coleccionClie solo use metodos de Coleccion:
```java
List<Cliente> listaClientes = new ArrayList<>();
Collection<Cliente> coleccionClie = listaClientes;
```

## Métodos de Inserción

- **add(E elem)**
  Añade `elem`. Devuelve `true` si la colección cambia.
  ```java
  Cliente clienteNuevo = new Cliente("123", "Juan");
  boolean resultado = coleccionClie.add(clienteNuevo); // Añade un nuevo cliente
  ```

## Métodos de Eliminación



- **remove(Object obj)**
  Elimina la primera instancia de `obj` de la colección. Devuelve `true` si la colección cambió.
  ```java
  coleccionClie.remove(clienteNuevo); // Elimina el cliente Juan si está en la colección
  ```
- **clear()**
  Elimina todos los elementos de la colección. La vacia
  ```java
  coleccionClie.clear(); // Elimina todos los elementos
  ```

## Métodos de Comprobación

- **size()**
  Devuelve el número de elementos en la colección.
  ```java
  int tamaño = coleccionClie.size(); // Devuelve el número de elementos
  ```
- **isEmpty()**
  Devuelve `true` si la colección está vacía.
  ```java
  boolean estaVacia = coleccionClie.isEmpty();
  ```
- **contains(Object obj)**
  Devuelve `true` si `obj` está. Busca por `equals`, por lo que depende unicamente del `compareTo` declarado en el objeto.
  ```java
  boolean contiene = coleccionClie.contains(clienteNuevo);
    boolean contiene = coleccionClie.contains(new Cliente("115","",""));
  ```

## Iteración

- **Iterator\<E\> iterator()**
  Devuelve un iterador sobre los elementos de la colección que nos sirve para recorrerla, E es el objeto que guarda la coleccion.
  ```java
  Iterator<Cliente> it = coleccionClie.iterator();
  while (it.hasNext()) {
      Cliente cliente = it.next();
      System.out.println(cliente);
  }
  ```

## Métodos globales de la interfaz Collection

- **containsAll(Collection\<?\> c)**
  Devuelve `true` si la colección contiene todos los elementos de la colección `c`.
  ```java
  Collection<Cliente> otrosClientes = new ArrayList<>();
  ... //rellenamos ese array.
  boolean contieneTodos = coleccionClie.containsAll(otrosClientes);
  ```
- **addAll(Collection\<? extends E\> c)**
  Añade todos los elementos en `c` a la colección. Devuelve `true` si la colección cambió. Si es una lista se añaden al final, aunque se repitan. 
  ```java
  coleccionClie.addAll(otrosClientes);
  ```
- **removeAll(Collection\<?\> c)**
  Elimina todos los elementos de la colección que también están contenidos en `c`. Devuelve `true` si la colección cambió.
  ```java
  coleccionClie.removeAll(otrosClientes);
  ```
- **retainAll(Collection\<?\> c)**
  Mantiene solo los elementos en la colección que también están en `c`. Devuelve `true` si la colección cambió.
  ```java
  coleccionClie.retainAll(otrosClientes);
  ```

## Conversión y Manipulación

- **Object\[\] toArray()**
  Devuelve un array que contiene todos los elementos de la colección.
  ```java
  Object[] elementos = coleccionClie.toArray();
  ```
- **\<T\> T\[\] toArray(T\[\] a)**
  Devuelve un array de tipo `T` con todos los elementos de la colección, es costumbre definirla con tamaño 0.
  ```java
  Cliente[] arrayClientes = coleccionClie.toArray(new Cliente[0]);
  ```

- **Arrays.asList(T... a)** Convierte un array en una lista inmutable con los elementos del array en el mismo orden. Aunque la lista resultante no permite añadir o eliminar elementos, se puede insertar en otra colección mutable. 

```java
Integer[] tabla = {1, 2, 3, 4, 5, 6};
Collection<Integer> lista = new ArrayList<>();
lista.addAll(Arrays.asList(tabla));
```

## Interface List
tanto `ArrayList` como `LinkedList` hacen lo mismo pero su rendimiento es diferente:
- `ArrayList` más rápida en operaciones de recorrer listas para lectura o modificación de ítems
- `LinkedList` mejor rendimiento con operaciones de inserción y eliminación de ítems.
### Métodos Específicos de List

La interfaz `List` extiende de `Collection` y proporciona métodos para manipular elementos con acceso posicional por índices.

- `.get(int index)` devuelve el elemento en la posición `index`. Ej:`listaEnteros.get(2)`
- `.set(int index, E element)` reemplaza el elemento en la posición `index` por `element`, y retorna el elemento original.
- `.add(int index, E element)` inserta `element` en la posición `index`, desplazando los elementos existentes hacia la derecha.
- `.addAll(int index, Collection<? extends E> c)` inserta todos los elementos de la colección `c` en la posición `index`.
- `.remove(int index)` elimina el elemento en la posición `index` y lo retorna. *No confundir con `.remove(obj elemento)` de la Interface collection que elimina el elemento no el elemento de la posición.
- `indexOf(Object o)` devuelve el índice de la primera ocurrencia de `o`.
- `lastIndexOf(Object o)` devuelve el índice de la última ocurrencia de `o`.
- `equals(Object o)` compara la lista con otra lista `o` para verificar si contienen los mismos elementos en el mismo orden.
- `sort(Comparator<? super E> c)` ordena la lista basándose en el comparador `c`. Si `c` es `null`, se utiliza el orden natural de los elementos (si son comparables).

Para el sort podemos usar una expresion lamda
```java
List<Integer> listaEnteros = new ArrayList<>(Arrays.asList(3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5));
listaEnteros.sort(Integer::compareTo); // Orden natural ascendente

```
# Interfaz Set

La interfaz `Set` también es una extensión de `Collection` pero no permite elementos duplicados y no garantiza el orden de los elementos, excepto en ciertas implementaciones:
No tiene metodos propios sino que usa los metodos de `Collection`

- `HashSet` no garantiza ningún orden.
- `TreeSet` ordena sus elementos según un criterio de ordenación (natural o un comparador proporcionado).
- `LinkedHashSet` mantiene el orden de inserción.

# Conversión Entre Colecciones

Para convertir entre diferentes tipos de colecciones, puedes utilizar los constructores y métodos adecuados para mantener o transformar la ordenación de los elementos.

## Ejemplos de Conversión

- Para obtener un `TreeSet` desde otro conjunto (por ejemplo, `HashSet` o `LinkedHashSet`), puedes usar dos métodos:
    - Directamente al constructor de `TreeSet` añadiendo elementos con `addAll()`.
    - Pasando el conjunto original al constructor de `TreeSet` si el ordenamiento natural es deseado.

```java
Set<Integer> conjuntoEnteros = new LinkedHashSet<>(Arrays.asList(4, 1, 5, 10, 3)); TreeSet<Integer> conjuntoOrdenado = new TreeSet<>(conjuntoEnteros); System.out.println(conjuntoOrdenado); // [1, 3, 4, 5, 10]
```
# Clase Collections

La clase `Collections` ofrece métodos estáticos para trabajar con colecciones, incluyendo utilidades para ordenar, buscar y modificar elementos.

## Ordenación

- `Collections.sort(List<T>)`: Ordena cualquier `List<T>` que implemente `Comparable`.
- `Collections.sort(List<T>, Comparator<? super T>)`: Ordena la lista según un `Comparator` proporcionado.

## Búsqueda

- `Collections.binarySearch(List<? extends Comparable<? super T>>, T)`: Realiza una búsqueda binaria en la lista ordenada.
- Para ordenar por un criterio no natural, usa el mismo comparador tanto para ordenar como para la búsqueda.
```java
List<Cliente> clientes = Arrays.asList(
		new Cliente("111", "Marta"),
		new Cliente("112", "Carlos") 
);
Collections.sort(clientes, Comparator.comparing(Cliente::getNombre)); 
int index = Collections.binarySearch(clientes, new Cliente("112", ""), Comparator.comparing(Cliente::getNombre));
```


## Manipulación de Datos

- `Collections.swap(List<?> list, int i, int j)`: Intercambia dos elementos.
- `Collections.replaceAll(List<T> list, T oldVal, T newVal)`: Reemplaza todos los ocurrencias de `oldVal` por `newVal`.
- `Collections.fill(List<? super T> list, T obj)`: Rellena la lista con el objeto `obj`.

```java
List<Integer> lista = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5)); Collections.fill(lista, 0);
```

## Utilidades

- `Collections.max(Collection<? extends T>)` y `Collections.min(Collection<? extends T>)`: Devuelven el máximo y mínimo elemento, respectivamente.
- `Collections.shuffle(List<?>)`: Desordena los elementos de la lista.

```java
List<Integer> datos = new ArrayList<>(Arrays.asList(1, 2, 3)); Collections.shuffle(datos); 
Integer max = Collections.max(datos);
```
`







 