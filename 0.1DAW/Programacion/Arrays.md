- `tabla.length` longitud
- `Arrays.equals(t1, t2)` compara, devuelve boolean.
## Declarar arrays

- `tipo [] variable = new tipo[longitud];`
- `int [] datos = {2, -3, 0 ,7};`

## For each
  ```java
  for (declaracion variable: tabla){
  ....
  }
  ```
  la variable declarada es del mismo tipo que la tabla
  ```java
  for (double = sueldo : sueldos){
  sumaSueldos+= sueldo;
  }
```

## Metodos

### Arrays.fill (rellena la tabla con default)
 `Arrays.fill(sueldos, 1234.56)` inicializa los elementos de un array a un valor.
 
 `Arrays.fill(sueldos,3,7,1234.56)` inicializamos desde 3 hasta 6 (no incluye el último)
### Arrays.toString (mostrar en string)

`Arrays.toString(tabla)` nos devuelve un string con el contenido.

## Arrays.sort (Ordenación)
Ordena
`Arrays.sort(tabla)` esta sobrecargado para todos los primitivos, para usar una clase se puede sobrecargar con el #Comparator.

## Busqueda

#### Secuencial (desordenada)

```java
/* búsqueda secuencial */
int claveBusqueda = loquebuscamos; // Asumo que tienes alguna clave de búsqueda definida
int[] t = new int[100]; // Asumo que tienes algún arreglo 't' definido

for (int i = 0; indiceBusqueda < t.length && t[indiceBusqueda] != claveBusqueda; i++) {

	if (i < t.length) {
	    // claveBusqueda se encuentra en la posición indiceBusqueda
	} else {
	    // el índice se ha salido de rango
	    // no encontrado
}
}

```

#### Binaria (ordenada) Arrays.binarySearch()

```java
int pos = Arrays.binarySearch(precios, 19.95);
if (pos >= 0) {
    System.out.println("Encontrado en el índice: " + pos);
} else {
    System.out.println("Lo sentimos, no se ha encontrado.");
}

```

## Arrays.copyOf & Arrays.copyOfRange

`a = Arrays.copyOf(t,3)` copia t con longitud 3. si es menor solo se copian los que caben y si es mayor se inicializan por defecto (0)

`a = Arrays.copyOfRange(t,3,7)` copia desde el indice 3 hasta el 6 (uno menos).

`Arrays.copy(object tablaOrigen, int posOrigen, Object tablaDestino, int posDestion, int longitud) 
- `Arrays.copy(t , 3, a, 6, 4)` copia t en a, desde 3 de t, y desde 6 en a, 4 indices. 

## Insercion

#### Inserccion no ordenada

`t = Arrays.copyOf(t, t.length+1);
`t[t.length+1] = nuevo

#### Inserccion ordenada

```java
int[] t = {1, 2, 3, 4, 6, 7, 8}; // Arreglo original
int nuevo = 5; // Nuevo elemento a insertar

// Usamos búsqueda binaria para encontrar la posición de inserción del nuevo elemento
int indiceInsercion = Arrays.binarySearch(t, nuevo);

// Si el elemento no existe en el arreglo, binarySearch retorna (-(punto de inserción) - 1)
if (indiceInsercion < 0) {
    indiceInsercion = -indiceInsercion - 1; // Convertimos a la posición correcta de inserción
}

// Creamos un nuevo arreglo con un espacio adicional
int[] copia = new int[t.length + 1];

// Copiamos los elementos del arreglo original hasta el punto de inserción en el nuevo arreglo
System.arraycopy(t, 0, copia, 0, indiceInsercion);

// Insertamos el nuevo elemento en el punto de inserción
copia[indiceInsercion] = nuevo;

// Copiamos el resto de elementos del arreglo original después del punto de inserción
System.arraycopy(t, indiceInsercion, copia, indiceInsercion + 1, t.length - indiceInsercion);

// Referenciamos t a la nueva tabla copia
t = copia;

// Mostramos el nuevo arreglo
System.out.println(Arrays.toString(t));

```
## Eliminación \*(escribir)

## Tablas n-dimensionales

`int datos[] []`
`datos = new int [5][5]`

```java
for (filas=0; filas<datos.length; i++){ //filas
	for (col=0; col<datos[filas].length; j++) //columnas
		datos[filas][col] = sc.nextInt();
}
```

