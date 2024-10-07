# Intro
Los sistemas de ficheros pueden ser de dos tipos:
- **Carácter** archivos y otras fuentes de texto
- **Binarios** bytes, manipulan cualquier tipo de datos.
---
# Excepciones
![[Pasted image 20240430171603.png]]
las excepciones de tipo **error** no se puede hacer nada por ellas y pararan la ejecución del código
las excepciones de **tiempo de ejecución** aka *runtime exceptions* se corrigen arreglando el código.

y luego están las excepciones de tipo **Exception** (subclase de **Throwable**) que son errores como entrada de datos de tipo equivocado, apertura de ficheros con rutas de acceso erróneas u operaciones aritméticas no permitidas. 

## Bloques try, catch, finally

Cuando un fragmento de código puede tener un error lo encerramos en un  ```try``` .
si salta una excepción la capturaremos en un ```catch``` a continuación y se interrumpirá la ejecución del bloque ```try``` lanzará el ```catch``` y continuara con el código que tengamos después del bloque ```try-catch``` . 

Peeero si tenemos un ```finally``` su contenido se lanzará si o también, aunque tengamos un `return` o lo que sea dentro, este tipo de bloque se suele usar para cerrar ficheros y demás sin importar si se han llegado a abrir o no.
```java 
try {
	int c;
	c = a/b;
	return;
}
catch (ArithmeticException ex){
			System.out.println("Error: divisón por cero");
			return;
}
finally {
	System.out.println("Tonto el que lo lea");
}
````

se puede usar varios metodos en el `catch` para capturar la excepción, como:
- `getMessage()`: mensaje descriptivo del error
- `toString()` : descripcion del error llamando al `toString` de la variable.
- - escribir lo que te salga del rabo.

se pueden poner más de un `catch` seguido concatenando diferentes tipos de excepciones, la norma es ir de lo mas especifico a lo general
```java
catch (ArithmeticException ex) {
	sout("Una excepcion aritmetica es mas concreta");
}
catch (Exception ex){
	sout("queuna excepcion a secas");
}
````

#### throws
podemos usar `throws` en un metodo para declarar que puede lanzar una determinada excepcion, y luego recogerla en un segundo metodo o lugar donde se utilice. o bien con un `try-catch` a secas. ejemplos:

##### `try-catch` 
```java
void metodo1(int a, int b) {
	int c;
	try {
		c= a/b;
	} catch (ArithmeticException ex) {
		sout("Division entre cero");
	}
}
void metodo2(){
	int x, y;
	metodo1(); //no hay necesidad de encapsularlo en un try-catch porque está ya en el metodo1.
}
````

#### `throws`
````java
void metodo1(int a, int b ) throws AritmeticException {
	int c;
	c = a/b;
	sout("a/b = "+ c);
}
void metodo2(){
	int x, y;
	try {
		metodo1(x,y);
	} catch (ArithmeticException ex) {
		sout("Division por cero");
	}	
}
````

## Requisito de captura o especificación

-  **excepciones comprobadas** *(checked exceptions)* excepciones comunes que hasta el ide te avisa de meter un `try-catch`  
- **excepciones no comprobadas** *(unchecked exceptions)* `ArithmeticException ArraysIndexOutofBoundsException` donde simplemente corregimos el codigo ****'cateto'***

> [!AVISO]
> Añadir un listado de Exceptions comunes 
> ej:
> `InputMismatchException` entrada de tipo de erroneo

## Excepciones de usuario `throw`
podemos crear nuestras propias excepciones, solo tenemos que crear una clase y heredar de `Exception`, después podemos usarla lanzandola con `throw` y creandola con `new`
```java
public class ExcepcionEdadNegativa extends Exception {
	public String toString(){
		return "Edad negativa";
	}
}
---
try {
	sout("Introducir edad: ");
	int edad = new Scanner(System.in).nextInt(); //captura directamenta al crear el escanner.
		if (edad<0){
			throw new ExceptionEdadNegativa(); //declaramos la excepcion
		} else {
			bla bla bla
		}
	} 	
} catch (ExcepcionEdadNegativa ex) {
		sout(ex);
}
````

# Flujos de entrada de texto
- `import java.io.*` <- importar todas las sentencias de Flujo de entrada de tipo texto.
- todas acaban en `Reader`
### FileReader

A los constructores se les pasa la ruta del archivo:
- puede ser absoluta:
`FileReader in = new FileReader(C:\\NetBeans\\Proyect1\\textos\\test.txt)`  
- o puede ser relativa:
- `FileReader in = new FileReader(textos\\test.txt)` *asumiendo que la estamos llamando desde Proyect1*
- `IOException` <-- excepción para cuando falla la apertura de flujo de entrada o salida.
 - `int read()`  <-- lee el fichero y devuelve el caracter unicode como entero. devuelve **-1** cuando acaba.
 - `void close()`<-- cerrar el fujo de entrada.
````java
>FileReader in = null;
try {
>	in = new FileReader("Main.java");
>	int c = in.read(); //va llamando al siguiente caracter cada vez que usamos in.read();
>	while (c!=-1){
>	texto = texto +(char) c;
>	c= in.read(); //llama al siguiente caracter
	}
} catch (IOException ex) {
	sout("ex.getMessage());
} finally {
	if (in != null) {
		try {
>			in.close();
		} catch (IOException ex) {
			sout(ex);
		}
	}
}
sout(texto);
````

### BufferedReader 

usa `FileReader` pero llamando a `BufferedReader` es más rapido porque hace menos accesos al disco.

`BufferedReader in = new BufferedReader (new FileReader("Main.java"));`

- `String readLine()` <- leemos el documento linea a linea en lugar de caracter a caracter al final devuelve un **null**.
```java
String texto ="";
>BufferedReader in = null;
try {
>	in = new BufferedReader (new FileReader("Main.java"));
>	String line = in.readLine();
>	while (line != null) {
>	texto= texto +line+ '\n'; //el salto de linea lo ponemos manual porque no lo lee
>	line = in.readLine();
	}
} catch (IOException ex) {
sout(ex.getMessage());
} finally {
	if (in != null) {
	try {
		in.close();
	} catch (IOException ex) {
		sout(ex);	
		}
	}
}
````

# Scanner y flujos de entrada

Con scanner recogemos lo que queramos usando `next` *loquesea* `()` sean int, dobule, ...
le podemos introducir los elementos queramos separados por **elementos en blanco** -espacios, tabuladores, saltos de linea- o secuencias de ellos. 
Ej: podemos pedir 5 ints, e intorducir uno intro, otro intro, otro intro... o bien 1 23 45 2 42 intro.
Scanner y nextInt() identificaran los enteros por las separaciones y los devuelve.

>[!useLocale]
> para que el `scanner` tome los decimales marcados por **.** hay que usar `.useLocale(Locale.US)`
> ej:
> `Scanner s = new Scanner(System.in).useLocale(Locale.US);`

#### `(System.in)`
Leido de teclado
#### `(loQueMeDeLaGana)` String
Le podemos pasar una cadena String o lo que queramos a un scanner para que el aplique los metodos de su clase. 
ej:
```java
String numeros = "1 34 46 23 67 346 73 2 1 6"
Scanner sc = new Scanner(numeros);

-------------------------------------

>BufferedReader in = null;
try {
>	in = new BufferedReader (new FileREader ("Numeros.txt"));
	Scanner sc;
	double numero;
	double suma = 0;
>	String linea = in.readLine();
	
>	while (linea != null {
>		sc = new Scanner (linea).useLocale(Locale.US);
>		if (sc.hasNextDouble()) { //si es un double
			numero =s.nextDouble();
			suma += numero;
		}
>		linea= in.readLine();
		}
	System.out.println("suma: "+ suma);
	} catch (IOException ex) {
		sout(ex.getMessage());
	} finally {
		if (in!= null) {
			try {
				in.close();
			} catch (IOException ex) {
				sout(ex);
			}
		}
	}
````

`.hasNextDouble()` <--lee el siguiente token de la cadena que le hemos pasado a Scanner y nos indica **sin consumir el token** si se trata de un Double (igual que doble estará int..etc...)

#### `(elArchivoDeTextoQueMeDeLaGana.txt)`

Podemos pasarle un fichero por ejemplo un archivo de texto donde hemos guardo una serie de numeros enteros.

```java
FileInputStream flujo = null;
try {
	flujo = newFileInputStream("Enteros.txt");
} catch (FileNotFoundException ex) {
	sout(ex.getMEssage());
}
Scanner sc = new Scanner(flujo);
int contador = 0;
int suma = 0;
while (sc.hasNext()) {
int n = sc.nextInt();
	sout(n+" ");
	suma += n;
	contador++;
}
double media = (double) suma / contador;
sout(bla bla bla);
````


>[FileInputStream]
>es una clase que permite leer datos de un archivo como un flujo de bytes, pero tambien vale para texto. 

>[FileNotFoundException]
es una subclase de IOException que nos dice que el archivo no se encuentra

# Flujos de salida de Texto

- todos acaban en `Writter`
### `FileWriter`

`FileWriter (String archivo)` <-- construye desde el principio y destruye lo anterior
`FileWriter (String  archivo, boolean noborrar` (true añadimos texto al final)

igual que los Reader hay que usar un `try-catch` para capturar una excepción de tipo `IOException` 

###  `BufferedWriter`

```java
BufferedWriter out;
out = new BufferedWriter (new FileWriter("salida.txt"));
````
usa:
- `void write (int caracter)` introduce un caracter en el archivo.
- `void write (String cadena)` introduce una cadena en el archivo.
- `void newLine()` escribe un salto de linea porque no se debe usar "\n"
- `void flush()` vacia el bufer y escribe los caracteres pendientes.
- `void close()` cierra el flujo y vacia el bufer.

```java
BufferedWriter out = null;
try {
	out = new BufferedWriter (new FileWriter("quijote.txt"));
	String cad = "En un lugar de la mancha,";
	for (int i=0; i<cad.length(); i++) {
		out.write(cad.charAt(i)); //caracter a caracter	
	}
	out.newLine(); //salto de linea
	cad = "de cuyo nombre no quiero acordarme."; 
	out.write(cad); //write con parametro cadena
} catch (IOException ex){
	sout(ex);
} finally {
	if (out!= null){
		try {
			out.close();
		} catch (IOException ex) {
			sout(ex);
		}
	}
}
````

#### `try-catch-resources`
es importante cerrar el flujo con `.close()` pero tampoco hay que rayarse mucho porque hay una estructura que se llama `try-catch-resources` que lo cierra pero hay que declararla  con un `()` después de `try`:

```java
try (BufferedWriter out = new BufferedWriter(new FileWriter("quijote.txt"))) {
	String cad = "En un lugar de la mancha,";
	for (int i=0; i<cad.length(); i++) {
		out.write(cad.charAt(i)); //caracter a caracter	
	}
	out.newLine(); //salto de linea
	cad = "de cuyo nombre no quiero acordarme."; 
	out.write(cad); //write con parametro cadena
} catch (IOException ex){
	sout(ex);
}
````

# Ficheros XML y Java.API JAXB

*Java Architecture for XML Binding*
- enlaza elementos XML con conjunto de clases y objetos de Java.
>[!DOM] DOM
>el modelo DOM no es otra cosa que los elementos anidadados tal y como se anidan en un XML que luego nos permitira acceder a ellos de una forma ordenada

Ejemplo:
```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<socio id="23">
    <nombre>Martin Fisher</nombre>
    <direccion>43 Bass St</direccion>
    <alta>12/12/2020</alta>
</socio>
````
 Para trabajar con el crearemos la clase `Socio` y anotaremos usando @Xml 
 - *importar `javax.xml.bind.annotation`**
 - `@XmlRootElement(name="socio")` para declarar el elemento raiz del XML
 - `@XmlType (propOrder = {atributoClase1, atributoClase2, atributoClase3 ...})` el orden en el que vamos a guardar con respecto al orden en el que aparecen en el XML
 - `@XmlAccessorType(XmlAccesType.FIELD)` los elementos se toman automaticamente de los atributos no estaticos de la clase -aunque sean privados- salvo que se delcaren como transitorios.
 -  `@XmlAccessorType(XmlAccesType.PROPERTY)` se toman de los getter y setter.
 - `@XmlAccessorType(XmlAccesType.PUBLIC_MEMBER)` de los publicos sean atributos o propiedades.

- `@XmlAttribute(name = "id", required = true)` encima del atributo, para indicar que recogemos el atributo de "id".
- `@XmlElement(name ="nombre")` nos traemos el elemento "nombre" al atributo.

```java
import javax.xml.bind.annotation.*;

>//ENCIMA DE LA DEFINICION DE CLASE
>	@XmlRootElement(name="socio") //INDICAMOS EL ELEMENTO RAIZ
>	@XmlType (porpOrder = {"nombreSocio","direccion","fechaAlta"})
>	@XmlAccessorType (XmlAccessType.FIELD)
public class Socio {
>	@XmlAttribute(name = "id", required=true)
>	private Integer identificacion;
>	@XmlElement(name ="nombre")
>	private String nombreSocio;
>	private String direccion; //no tiene anotacion @Xml, por lo que tomará un elemento con el mismo nombre <direccion>
>	@XmlElement(name = "alta")
>	private String fechaAlta;

	public Socio(){
	}
	public Socio (Integer identificacion, String nombreSocio, String direccion, String fechaAlta) {
		this.identificacion = identificacion;
		this.nombreSocio = nombreSocio;
		this.direccion = direccion;
		this.fechaAlta = fechaAlta;
	}
}
````

### `JAXBContext` 
no tiene constructor tiene un metodo estatico `newInstance()`
- `Marshaller` para agrupar (escribir en un XL)
- `Unmarshaller` desagrupar (leer un documento XML y crear objetos `Socio`)

#### `UnMarshaller`

```java
//CREAMOS EL CONTEXTO JAXB CON LA CLASE SOCIO
JAXBContext contexto = JAXBcontext.newInstance(Socio.class);
//CREAMOS EL UNMARSHALLER PARA EL CONTEXTO DE JAXB
Unmarshaller um = contexto.createUnmarshaller();
//DESERIALIZAMOS EL ARCHIVO XML A UN OBJETO JAVA 
//¡IMPORTANTE EL CASTEO A SOCIO!
Socio s = (Socio) um.unmarshal(newFile("socio.xml"));
````

#### `Marshaller`

con el marshaller necesitamos apoyarnos de `.setProperty` para configurar un formato!

```java
//CREAMOS EL MARSHALLER DESDE EL CONTEXTO JAXB
Marshaller m = contexto.createMarshaller();
//CREAMOS UN OBJETO DE LA CLASE SOCIO
Socio s1 =  new Socio(1, "Pepito Perez", "C/Desengaño 1", "01/09/2020");
//CONFIGURACION DEL MARSHALLER PARA QUE DE UN FORMATO
m.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, Boolean.TRUE);
//SERIALIZADO DEL OBJETO s1 A XML Y CREANDOLO EN "socio.xml"
m.marchal(s1, new FileWriter("socio1.xml"));
-----------------------------------------------------------------------------
//SI SOLO QUEREMOS VISUALIZAR EL XML SIN CREAR ARCHIVO PODEMOS USAR SYSTEM.OUT
m.marchal(s1, System.out);

````

#### XML complejos Wrapper y Transient
Wrapper es u *"Envoltorio* de nombre X que contrandra otros elementos en su interior, lo podemos usar para arrays de objetos que van a tener sus movidas dentro.

Trasient lo usamos para atributos que no queremos que se exporten al XML y que no están en el y vamos a recoger como `null`

```java
import java.util.Arrays;
import javax.xml.bind.annotation.*;

@XmlRootElement(name = "club")
@XmlType(propOrder = {"nombreClub", "listaSocios"})
@XmlAccessorType(XmlAccessType.FIELD)
public class Club {
    @XmlElement(name = "nombre")
    private String nombreClub;

>// AQUI VAMOS A METER UNA "LISTA DE SOCIOS" POR LO QUE USAMOS UN WRAPPER
>    @XmlElementWrapper(name = "socios")
>    @XmlElement(name = "socio")
>    private Socio[] listaSocios;

>// EL NIF NO QUEREMOS QUE SE REGISTRE Y NI APARECE EN EL XML
>    @XmlTransient
>   private String nif;

    public Club() {}

    public Club(String nombreClub, String nif) {
        this.nombreClub = nombreClub;
        this.listaSocios = new Socio[0];
        this.nif = nif;
    }

    public void nuevoSocio(Socio nuevo) {
        listaSocios = Arrays.copyOf(listaSocios, listaSocios.length + 1);
        listaSocios[listaSocios.length - 1] = nuevo;
    }
}
````

