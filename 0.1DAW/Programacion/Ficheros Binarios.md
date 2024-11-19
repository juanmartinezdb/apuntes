# Intro

importar `java.io`

Dos clases básicas para la **SERIALIZACIÓN Y DESERAILZACIÓN** de datos:
- `FileOutputStream` -- `ObjectOutputStream`
- `FileInputStream`  -- `ObjectInputStream`
# Flujos de salida binarios

```java
// Crear un archivo de salida para almacenar los datos serializados.
FileOutputStream archivo = new FileOutputStream("enteros.dat");

// Configurar un ObjectOutputStream para serializar objetos en el archivo creado.
ObjectOutputStream out = new ObjectOutputStream(archivo);

````

## Interface `Serializable`
para serializar archivos a bytes, se necesita de esta interface.  Hay clases como `String`, las colecciones y los arrays ya la traen implementada.

las clases que implementan `Serializable` no es necesario que implementen ningún metodo adicional, con declararla es suficiente

```java
class miClase implements Serializable {
	bla bla bla bla bla
}
````

## `ObjectOutputStream`

Métodos:
- `void writeBoolean(boolean b)` escribe un valor boolean en el fujo.
- `void writeChar(int c)` escribe el valor `char` quie ocupa los dos bytes menos significativos del valor entero que se le pasa como parámetro.
- `void writeInt(int n)` escribe un entero
- `void writeLong(long n)` escribe un entero largo
- `void writeDouble(double d)` escribe un número de tipo `double`
- `void writeObject(Object o)` escribe un objeto serializable. (esto incluye `String` o arrays )

```java
//QUEREMOS ESCRIBIR EN UN DATOS.DAT LOS VLAORES DE UNA TABLA DE DIEZ ENTEROS
int[] t = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
>ObjectOutputStream flujoSalida = null;
//LO METEMOS EN UN TRY CATCH PORQUE PUEDE GENERAR UNA EXCEPCION DE TIPO IOEXCEPTION
try { 
//CONCATENAMOS LA CREACION DEL FLUJO
>    flujoSalida = new ObjectOutputStream(new FileOutputStream("datos.dat"));
>    for (int n : t) { 
>        flujoSalida.writeInt(n); //METODO
>        ----ALTERNATIVA AL FOR------
>    //Como un array de enteros es un objeto en si, podriamos haber usado DIRECTAMENTE:
>       flujoSalida.writeObject(t)
>       -----------------------------
    }
} catch (IOException ex) {
    System.out.println(ex);
} finally {
    if (flujoSalida != null) {
        try {
            flujoSalida.close();
        } catch (IOException ex) {
            System.out.println(ex);
        }
    }
}
````

Ejemplo con cadena y l `try-catch-resources` que vimos en el tema 10 y que no cesita de un `finally` para cerrar el flujo
```java
String estrofa = "Con diez cañones por banda, \n"
               + "viento en popa a toda vela, \n"
               + "no corta el mar, sino vuela \n"
               + "un velero bergantín.";
>try (ObjectOutputStream out = new ObjectOutputStream(new >FileOutputStream("canconPirata.dat"))) {
>    out.writeObject(estrofa);
>} catch (IOException ex) {
>    System.out.println(ex);
}
````

# Flujos de entrada binarios

```java
ObjectInputStream flujoEntrada = new ObjectInputStream(new FileInputStream("datos.dat));
````

## `ObjectInputStream`

Tiene los mismos metodos que `ObjectOutputStream` pero con `read` 
Métodos:
- `void readBoolean()` llee un boolean de flujo de entrda.
- `void readChar()` lee un carácter
- `void readInt()` lee un entero
- `void readLong()` lee un entero largo
- `void readDouble()` lee un número de tipo `double`
- `void readObject()` lee un objeto. Si hemos guardado arrays como Objetos en lugar de sus primitivos, podemos leerlos usando `readObject()`.

```java
try (ObjectInputStream flujoEntrada = new ObjectInputStream(new FileInputStream("datos.dat"))) {
	// CASTEAMOS EL OBJETO  A int[]
    int[] tabla = (int[]) flujoEntrada.readObject(); 
    System.out.println(Arrays.toString(tabla));
} catch (IOException e) {
    System.out.println("Error de entrada/salida");
	//POR SI LO GUARDAMOS COMO INTS U OTRO TIPO DIFERENTE A OBJETO O QUE LA CLASE NO ESTÉ IMPORTADA O NO SEA VISIBLE
} catch (ClassNotFoundException e) { 
    System.out.println("El fichero no almacena un objeto tabla");
}
-------------------------------------------
lo mismo si trabajaos con un String 

try {
	String cadena = (String) flujoEntrada.readObject(); //CASTEAMOS EL OBJETO A STRING
} catch (ClassNotFoundException ex){
	sout(ex.getMessage);
}
````

## `EOFException` *End of File Exception*

si no sabemos donde acaba el fichero lo leeremos hasta encontrar `EOFException` que salta al llegar al final

```java
try {
	while (true){ //esto es una burrada, es un bucle infinito, no lo hagais en clase
		System.out.println(in.readInt());
	} catch (EOFException ex) {
		System.out.println("Fin de fichero");
	}
}
````

>[! OJO] OJITO!
>Cuando guardamos objetos que tienen referencias a otros objetos, no solo se guarda la referencia (es decir, la dirección de memoria), sino toda la información necesaria para reconstruir el objeto y sus relaciones al leer el archivo de nuevo. Esto incluye tanto los datos del objeto principal como los de los objetos referenciados. Java, por ejemplo, rastrea y guarda todas las referencias para poder reconstruir completamente la estructura y los datos cuando se leen posteriormente con `readObject()`.




