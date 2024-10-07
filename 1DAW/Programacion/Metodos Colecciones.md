- **Object\[\] toArray()** Devuelve un array con todos los elementos de la colección
`  Object[] elementos = coleccionClie.toArray();
- **\<T\> T\[\] toArray(T\[\] a)** Devuelve array T con los elementos de la coleccion( se suele iniciar a 0).
  `Cliente[] arrayClientes = coleccionClie.toArray(new Cliente[0]);
  - **Arrays.asList(T... a)** Array a lista INMUTABLE, pero se puede pasar a otro lista que si. 
  ```java
Integer[] tabla = {1, 2, 3, 4, 5, 6};
Collection<Integer> lista = new ArrayList<>();
lista.addAll(Arrays.asList(tabla));//usamos el INMUTABLE para rellenar la lista que si podemos trabajar.
```

## Conversión entre Colecciones
>`Collection<T> coleccion = new TipoDeColeccion<>(Arrays.asList(elementos));
>`OtraColeccion<T> nuevaColeccion = new TipoDeNuevaColeccion<>(coleccion);
		ej:
```java
Set<Integer> conjunto = new HashSet<>(Arrays.asList(4, 1, 5, 10, 3));
Set<Integer> conjuntoOrdenado = new TreeSet<>(conjunto);

List<Integer> lista = new ArrayList<>(conjunto);
Set<Integer> conjuntoSinDuplicados = new LinkedHashSet<>(lista);
```
# Collections (todas)
- **add(E elem)**
- **remove(Object obj)**
- **clear()**
- **size()**
- **isEmpty()**
- **contains(Object obj)**
### Iterator
- **Iterator\<E\> iterator()**
	- it.hasNext()
	- it.next()
	- it.remove()
## Collections (Globales)
- **containsAll(Collection\<?\> c)**  Verifica si contiene todos
 `Boolean contieneTodos = coleccionClie.containsAll(otrosClientes);
- **addAll(Collection\<? extends E\> c)** Añade todos los elementos
 ` coleccionClie.addAll(otrosClientes);
- **removeAll(Collection\<?\> c)** Elimina todos los elementos presentes en otra colección
`  coleccionClie.removeAll(otrosClientes);
- **retainAll(Collection\<?\> c)**  Conserva solo los elementos que están en otra colección
`coleccionClie.retainAll(otrosClientes);

# List

- `.get(int i)` devuelve el elem en la pos `i`. 
	-`lista.get(2)` 
- `.set(int i, E e)` reemplaza el elem en la pos `i` por `e`, y retorna el elem original. 
	- `lista.set(2, 10)` 
- `.add(int i, E e)` inserta `e` en la pos `i`, desplazando los elems existentes a la derecha. 
	- `lista.add(2, 20)` 
- `.addAll(int i, Collection<? extends E> c)` inserta todos los elems de la colección `c` en la pos `i`. 
	- `lista.addAll(2, col)` 
- `.remove(int i)` elimina el elem en la pos `i` y lo retorna. 
	- `lista.remove(2)` 
- `.indexOf(Object o)` devuelve el índice de la primera ocurrencia de `o`. 
	- `lista.indexOf(10)`
- `.lastIndexOf(Object o)` devuelve el índice de la última ocurrencia de `o`. 
	- `lista.lastIndexOf(10)` 
- `.equals(Object o)` compara la lista con otra lista `o` para verificar si contienen los mismos elems en el mismo orden. 
	- `lista.equals(otraLista)` 
- `.sort(Comparator<? super E> c)` ordena la lista basándose en el comparador `c`. Si `c` es `null`, usa el orden natural. 
	- `lista.sort(null)`
	- `listaEnteros.sort(Comparator.reverseOrder());
	- `listaPersonas.sort(Comparator.comparingInt(Persona::getEdad));
	- `listaPersonas.sort(Comparator.comparing(Persona::getNombre));`
	- `listaEnteros.sort((a, b) -> a.compareTo(b));

>[!Lambda]
Para el sort podemos usar una expresion lamda
```java
List<Integer> listaEnteros = new ArrayList<>(Arrays.asList(3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5));
listaEnteros.sort(Integer::compareTo); // Orden natural ascendente
```

# Set  
>[!Tipos] 
>- `HashSet` no garantiza ningún orden.
>- `TreeSet` ordena sus elementos según un criterio de ordenación (natural o con comparador).
>- `LinkedHashSet` mantiene el orden de inserción.
>Set no tiene metodos propios, solo utiliza los heredados de Collection

# Collections. (la Clase)

- `Collections.sort(lista)` ordena `lista` en orden natural. 
- `Collections.sort(lista, c)` ordena `lista` con el comparador `c`. 
- `int i = Collections.binarySearch(list, clave)` busca `clave` en `list` ordenada. 
-  `int i = Collections.binarySearch(list, clave, c)` busca `clave` en `list` ordenada con el comparador `c`. 
- `Collections.swap(list, i, j)` intercambia elementos en `i` y `j`. 
- `Collections.replaceAll(list, antiguo, nuevo)` reemplaza `antiguo` por `nuevo` en `list`. 
- `Collections.fill(list, valorRelleno)` rellena `list` con `valorRelleno`. 
- `Collections.copy(dest, src)` copia `src` a `dest`. 
- `Collections.shuffle(list)` desordena `list`. 
- `int freq = Collections.frequency(col, obj)` cuenta ocurrencias de `obj` en `col`. 
- `T max = Collections.max(col)` devuelve el máximo en `col`. 
- `T max = Collections.max(col, comp)` devuelve el máximo en `col` usando `comp`. 
- `Collections.reverse(list)` invierte el orden de `list`. 
- `Set<T> singleton = Collections.singleton(elem)` devuelve un conjunto con solo `elem`. 
##  Metodos de Collections (Extendida)
- `Collections.sort(List<T> lista)` ordena `lista` en orden natural. 
	- `Collections.sort(lista)`
- `Collections.sort(List<T> lista, Comparator<? super T> c)` ordena `lista` con el comparador `c`. 
	- `Collections.sort(lista, c)`
- `Collections.binarySearch(List<? extends T> list, T clave)` busca `clave` en `list` ordenada. 
	- `int i = Collections.binarySearch(list, clave)`
- `Collections.binarySearch(List<? extends T> list, T clave, Comparator<? super T> c)` busca `clave` en `list` ordenada con el comparador `c`. 
	- `int i = Collections.binarySearch(list, clave, c)`
- `Collections.swap(List<?> list, int i, int j)` intercambia elementos en `i` y `j`. 
	- `Collections.swap(list, i, j)`
- `Collections.replaceAll(List<T> list, T antiguo, T nuevo)` reemplaza `antiguo` por `nuevo` en `list`. 
	- `Collections.replaceAll(list, antiguo, nuevo)`
- `Collections.fill(List<? super T> list, T valorRelleno)` rellena `list` con `valorRelleno`. 
	- `Collections.fill(list, valorRelleno)`
- `Collections.copy(List<? super T> dest, List<? extends T> src)` copia `src` a `dest`. 
	- `Collections.copy(dest, src)`
- `Collections.shuffle(List<?> list)` desordena `list`. 
	- `Collections.shuffle(list)`
- `Collections.frequency(Collection<?> col, Object obj)` cuenta ocurrencias de `obj` en `col`. 
	- `int freq = Collections.frequency(col, obj)`
- `Collections.max(Collection<? extends T> col)` devuelve el máximo en `col`. 
	- `T max = Collections.max(col)`
- `Collections.max(Collection<? extends T> col, Comparator<? super T> comp)` devuelve el máximo en `col` usando `comp`. 
	- `T max = Collections.max(col, comp)`
- `Collections.reverse(List<?> list)` invierte el orden de `list`. 
	- `Collections.reverse(list)`
- `Collections.singleton(T elem)` devuelve un conjunto con solo `elem`. 
	- `Set<T> singleton = Collections.singleton(elem)`
# MAPS

`Map<K, V> m = new HashMap<>();` No garantiza orden
`Map<K, V> m = new TreeMap<>();` Se ordena según orden natural o comparator
`Map<K, V> m = new LinkedHashMap<>();` Se ordenan por inserción.


### Métodos Específicos de Map

- `V .put(clave, valor)` inserta `clave` y `valor`, retorna el valor anterior o `null`.
- `V .remove(clave)` elimina la entrada con `clave`, retorna el valor asociado o `null`.
- `.clear()` elimina todas las entradas.
- `V .get(clave)` retorna el valor asociado a `clave` o `null`.
- `Bo .containsKey(clave)` devuelve `true` si existe una entrada con `clave`.
- `Bo .containsValue(valor)` devuelve `true` si existe una entrada con `valor`.
- `SK .keySet()` retorna un `Set` con todas las claves.
- `CV .values()` retorna una `Collection` con todos los valores.
- `Set<Map.Entry<K,V>> .entrySet()` retorna un `Set` con todas las entradas `Map.Entry<K, V>`.
- `V .putIfAbsent(clave, valor)` inserta `clave` y `valor` si `clave` no está presente, retorna el valor actual o `null`.
- `Bo .replace(clave, valorAntiguo, valorNuevo)` reemplaza `valorAntiguo` por `valorNuevo` si está asociado a `clave`, retorna `true` si se reemplazó.
- `V .replace(clave, valor)` reemplaza el valor asociado a `clave` por `valor`, retorna el valor antiguo o `null`.
- ` .forEach((clave, valor) -> { ... })` ejecuta `accion` para cada entrada.
	- `map.forEach((clave, valor) -> System.out.println(clave + "=" + valor));
- ` .replaceAll((clave, valor) -> { ... })` reemplaza cada valor con el resultado de `funcion`. Ej: `map.replaceAll((clave, valor) -> valor + 1);
- `Bo .isEmpty()` devuelve `true` si el mapa está vacío.
- `Int.size()` retorna el número de entradas en el mapa.
- `Bo .equals(o)` compara el mapa con `o` para verificar si contienen las mismas entradas.
- ` .hashCode()` retorna el hash code del mapa.
## Metodos  MAPS extendida:
- `V put(K clave, V valor)` inserta `clave` y `valor`, retorna el valor anterior o `null`. 
	- `map.put(clave, valor)`
- `V remove(Object clave)` elimina la entrada con `clave`, retorna el valor asociado o `null`. 
	- `map.remove(clave)`
- `void clear()` elimina todas las entradas. 
	- `map.clear()`
- `V get(Object clave)` retorna el valor asociado a `clave` o `null`. 
	- `map.get(clave)`
- `boolean containsKey(Object clave)` devuelve `true` si existe una entrada con `clave`. 
	- `map.containsKey(clave)`
- `boolean containsValue(Object valor)` devuelve `true` si existe una entrada con `valor`. 
	- `map.containsValue(valor)`
- `Set<K> keySet()` retorna un `Set` con todas las claves. 
	- `Set<K> claves = map.keySet()`
- `Collection<V> values()` retorna una `Collection` con todos los valores. 
	- `Collection<V> valores = map.values()`
- `Set<Map.Entry<K, V>> entrySet()` retorna un `Set` con todas las entradas `Map.Entry<K, V>`.
	- `Set<Map.Entry<K, V>> entradas = map.entrySet()`
- `V putIfAbsent(K clave, V valor)` inserta `clave` y `valor` si `clave` no está presente, retorna el valor actual o `null`. 
	- `map.putIfAbsent(clave, valor)`
- `boolean replace(K clave, V valorAntiguo, V valorNuevo)` reemplaza `valorAntiguo` por `valorNuevo` si está asociado a `clave`, retorna `true` si se reemplazó. 
	- `map.replace(clave, valorAntiguo, valorNuevo)`
- `V replace(K clave, V valor)` reemplaza el valor asociado a `clave` por `valor`, retorna el valor antiguo o `null`. 
	- `map.replace(clave, valor)`
- `void forEach(BiConsumer<? super K, ? super V> accion)` ejecuta `accion` para cada entrada. 
	- `map.forEach((clave, valor) -> { ... })`
- `void replaceAll(BiFunction<? super K, ? super V, ? extends V> funcion)` reemplaza cada valor con el resultado de `funcion`. 
	- `map.replaceAll((clave, valor) -> { ... })`
- `boolean isEmpty()` devuelve `true` si el mapa está vacío. 
- `int size()` retorna el número de entradas en el mapa. 
- `boolean equals(Object o)` compara el mapa con `o` para verificar si contienen las mismas entradas. 
	- `map.equals(o)`
- `int hashCode()` retorna el hash code del mapa. 
	- `map.hashCode()`