# JavaServer Pages (JSP)

Los **servlets** tienen algunas limitaciones que dificultan la gestión de contenido HTML. Primero, todas las etiquetas HTML dentro de un servlet deben ser encerradas en cadenas de caracteres Java, lo cual hace que generar respuestas HTTP sea una tarea tediosa y propensa a errores. Además, todas las etiquetas HTML se codifican directamente en los servlets, lo cual dificulta la modificación del diseño sin afectar el código.

**JavaServer Pages (JSP)** soluciona estos problemas al complementar a los servlets. Las aplicaciones web modernas en Java suelen combinar tanto servlets como páginas JSP, aprovechando lo mejor de cada tecnología.

## Visión General de JSP

Una página JSP es esencialmente un servlet, pero trabajar con JSP es más sencillo por varias razones:

1. No es necesario compilar manualmente las páginas JSP. El contenedor se encarga de la compilación automáticamente la primera vez que la página se solicita.
2. Las páginas JSP son archivos de texto con extensión `.jsp`, que se pueden editar con cualquier editor de texto, lo cual facilita su desarrollo y mantenimiento.

Las páginas JSP se ejecutan en un **contenedor JSP**. Normalmente, un contenedor de servlets también puede funcionar como contenedor JSP, como es el caso de **Apache Tomcat** o **Jetty**.

### Funcionamiento Interno de JSP

La primera vez que una página JSP es solicitada, el contenedor JSP realiza dos pasos principales:

1. **Traducción**: La página JSP se traduce en una clase que implementa la interfaz **JspPage** o su subinterfaz **HttpJspPage**. Al ser una subinterfaz de **Servlet**, cada página JSP es, técnicamente, un servlet. Si ocurre algún error durante la traducción, se envía un mensaje de error al cliente.
2. **Compilación**: Si la traducción es exitosa, el contenedor compila la clase en un servlet y lo carga en memoria, ejecutando los mismos ciclos de vida que para un servlet tradicional (métodos `init`, `service` y `destroy`).

Para las peticiones posteriores a la misma página JSP, el contenedor revisa si la página ha sido modificada. Si no ha cambiado, se utiliza el servlet JSP que ya está cargado en memoria, lo cual hace que las peticiones sucesivas sean mucho más rápidas.

Para evitar la latencia de la primera carga de las páginas JSP, se pueden tomar dos enfoques:

- **Precompilar las páginas JSP** y desplegarlas como servlets, lo cual acelera la carga inicial.
- Configurar la aplicación para que todas las páginas JSP se compilen al arrancar la aplicación (usando el elemento `<load-on-startup>` en el descriptor de despliegue).

### Plantillas de Datos y Elementos Sintácticos

Una página JSP puede contener **plantillas de datos** y **elementos sintácticos**:

- **Plantillas de Datos**: Son elementos que no tienen un significado especial para el traductor JSP, como etiquetas HTML o texto. Estos elementos se envían tal cual al navegador.
- **Elementos Sintácticos**: Representan bloques de código Java u otras instrucciones para el traductor JSP. Por ejemplo, `<%` indica el comienzo de un bloque de código Java, y `%>` indica su final. Estos bloques de código se denominan **scriplets**.

Otra diferencia con los servlets es que una página JSP no necesita ser anotada ni mapeada en el descriptor de despliegue. Cada página JSP es accesible a través de su ruta directamente en el navegador, salvo que se encuentre bajo el directorio **WEB-INF**, en cuyo caso no será accesible desde fuera.

### Código Java en JSP

El código Java puede aparecer en cualquier parte de una página JSP, siempre que esté encerrado entre `<%` y `%>`. Además, para importar clases Java, se usa la directiva **@page** con el atributo **import**:

```jsp
<%@ page import="java.util.List, com.miempresa.modelo.Producto" %>
```

Esto permite usar las clases directamente sin necesidad de especificar el nombre completamente cualificado.

### Objetos Implícitos

En JSP, los objetos que normalmente se pasarían explícitamente al servlet se encuentran disponibles automáticamente como **objetos implícitos**. Estos objetos incluyen:

| Objeto       | Tipo                                          |
|--------------|----------------------------------------------|
| **request**  | `javax.servlet.http.HttpServletRequest`       |
| **response** | `javax.servlet.http.HttpServletResponse`      |
| **out**      | `javax.servlet.jsp.JspWriter`                |
| **session**  | `javax.servlet.http.HttpSession`             |
| **application** | `javax.servlet.ServletContext`            |
| **config**   | `javax.servlet.ServletConfig`                |
| **pageContext** | `javax.servlet.jsp.PageContext`           |
| **page**     | `javax.servlet.jsp.HttpJspPage`              |
| **exception** | `java.lang.Throwable`                       |

- **pageContext**: Hace referencia al objeto `PageContext`, que proporciona información del contexto y acceso a varios otros objetos relacionados. Los atributos pueden ser almacenados en diferentes ámbitos: página, petición, sesión, y aplicación.

### Ámbitos en JSP

Los atributos en JSP pueden ser almacenados en cuatro ámbitos diferentes:

1. **PAGE_SCOPE**: Disponible solo en la misma página JSP.
2. **REQUEST_SCOPE**: Disponible durante el ciclo de vida de una petición.
3. **SESSION_SCOPE**: Disponible durante la vida de la sesión del usuario.
4. **APPLICATION_SCOPE**: Disponible para toda la aplicación.

El método `setAttribute` de `PageContext` permite establecer atributos en un ámbito específico:

```jsp
<%
    pageContext.setAttribute("producto", producto, PageContext.REQUEST_SCOPE);
%>
```

Esto tiene el mismo efecto que:

```jsp
<%
    request.setAttribute("producto", producto);
%>
```

### Uso del Objeto `out`

El objeto implícito **out** se refiere a la clase `JspWriter`, que es similar a `PrintWriter`, permitiendo enviar contenido al cliente. Se puede llamar a sus métodos sobrecargados como `print` o `println` para escribir directamente en la respuesta:

```jsp
<%
    out.println("Bienvenido al sistema");
%>
```

El compilador JSP establece por defecto el tipo de contenido como **text/html**. Si se desea enviar otro tipo de contenido, se debe especificar llamando a `response.setContentType` o usando la directiva **@page**.

```jsp
<%@ page contentType="application/json" %>
```

### Lenguaje de Expresiones (Expression Language - EL)

Las JSP también soportan **Expression Language (EL)**, lo cual simplifica el acceso a los datos sin necesidad de escribir scriplets. EL permite acceder a objetos y atributos usando una sintaxis más limpia:

```jsp
${producto.nombre}
```

Esto reemplaza la necesidad de escribir código Java para acceder a los atributos, haciendo que las páginas sean más legibles y fáciles de mantener.

## Conclusión

**JavaServer Pages (JSP)** proporcionan una forma sencilla de generar contenido dinámico en aplicaciones Java. Aunque funcionan bajo el capó como servlets, su sintaxis facilita la separación entre la lógica de negocio y la presentación, haciendo que el desarrollo de aplicaciones web sea más accesible para desarrolladores y diseñadores.

La combinación de JSP y servlets, junto con el uso adecuado de objetos implícitos, ámbitos y Expression Language, es fundamental para desarrollar aplicaciones web robustas, mantenibles y escalables en el entorno Java actual.

# Directivas en JSP

Las **directivas** son un tipo de elementos sintácticos en **JSP** que proporcionan instrucciones al traductor sobre cómo debe traducirse la página JSP en un servlet. Las directivas afectan a la configuración general de la página y determinan ciertos aspectos del comportamiento del servlet generado. Las dos directivas más importantes son **`page`** e **`include`**.

## Directiva `page`

La directiva **`@page`** se usa para dar instrucciones al traductor JSP sobre diversos aspectos de la página JSP actual. La sintaxis de esta directiva es:

```jsp
<%@ page atributo1="valor1" atributo2="valor2" ... %>
```

Algunos de los atributos más importantes de la directiva **`@page`** son:

- **import**: Especifica una o más clases Java que serán importadas y utilizables dentro de la página. Se puede usar el carácter comodín `*` para importar todo un paquete. Algunos paquetes como `java.lang`, `javax.servlet`, `javax.servlet.http` y `javax.servlet.jsp` ya se importan automáticamente.
- **contentType**: Especifica el tipo de contenido del objeto `response`. Por defecto, es `"text/html"`, pero puede cambiarse a otros valores como `"application/json"`.
- **pageEncoding**: Define la codificación de caracteres de la página. Por defecto, el valor es **ISO-8859-1**, pero se recomienda usar **UTF-8** para una mejor compatibilidad.
- **isELIgnored**: Indica si el Lenguaje de Expresión (EL) debe ser ignorado en la página.
- **language**: Especifica el lenguaje de scripting utilizado. En JSP 2.2, el único valor posible es **java**.

### Uso de la Directiva `@page`

La directiva `@page` puede aparecer en cualquier parte de la página JSP. Sin embargo, si la página incluye atributos como **`contentType`** o **`pageEncoding`**, estos deben colocarse antes de enviar cualquier contenido al cliente para asegurar que se configuran adecuadamente.

La directiva **`@page`** también puede repetirse en una página, pero los valores de los atributos (excepto **import**) deben coincidir. Si **import** se especifica varias veces, su efecto es acumulativo:

```jsp
<%@ page import="java.util.ArrayList" %>
<%@ page import="java.util.Date" %>
```

Esto es equivalente a:

```jsp
<%@ page import="java.util.ArrayList, java.util.Date" %>
```

## Directiva `include`

La directiva **`@include`** se usa para incluir contenido de otro archivo dentro de la página JSP. La sintaxis es la siguiente:

```jsp
<%@ include file="url" %>
```

Donde **`file`** representa la ruta relativa del archivo a incluir. Si la ruta comienza con `/`, se interpreta como una ruta absoluta en el servidor; de lo contrario, es relativa a la ubicación de la página JSP actual.

Por convención, los archivos que se incluyen suelen tener la extensión **`.jspf`** para indicar que son **fragmentos JSP**. También se pueden incluir archivos HTML estáticos.

### Diferencia entre la Directiva `include` y la Acción `include`

- **Directiva `include`**: La inclusión ocurre en el momento de **traducción**. Esto significa que el contenido del archivo incluido se añade al servlet generado durante la compilación.
- **Acción `include`** (`<jsp:include>`): La inclusión ocurre en **tiempo de ejecución**, permitiendo una mayor flexibilidad. Los parámetros pueden pasarse al recurso incluido durante la petición, lo cual no es posible con la directiva `include`.

## Elementos de Scripting en JSP

Los elementos de scripting permiten escribir código Java directamente en una página JSP. Existen tres tipos de elementos de scripting: **scriptlets**, **declaraciones** y **expresiones**.

### Scriptlets

Un **scriptlet** es un bloque de código Java que comienza con `<%` y termina con `%>`.

```jsp
<%
    String nombre = "Juan";
    out.println("Bienvenido, " + nombre);
%>
```

Las variables definidas en un scriptlet son visibles en otros scriptlets dentro de la misma página.

### Expresiones JSP

Una **expresión JSP** es evaluada y su resultado se envía automáticamente al cliente mediante el método `print` del objeto `out`. Una expresión comienza con `<%=` y termina con `%>`.

```jsp
Hoy es <%= java.util.Calendar.getInstance().getTime() %>
```

No es necesario colocar un punto y coma al final de la expresión. El contenedor JSP evalúa la expresión y el resultado se envía al cliente de manera similar a un `out.print()`.

### Declaraciones

Las **declaraciones** se usan para definir variables y métodos que estarán disponibles en la página JSP. Se encierran entre `<%!` y `%>`.

```jsp
<%! public java.util.Date getFechaHoy() {
    return new java.util.Date();
} %>

<html>
<head>
<title>Declaraciones</title>
</head>
<body>
Hoy es <%= getFechaHoy() %>
</body>
</html>
```

Las declaraciones pueden colocarse en cualquier parte de la página y se pueden usar para sobrescribir los métodos `jspInit` y `jspDestroy`:

- **`jspInit`**: Similar al método `init` de los servlets, se llama cuando la página JSP se inicializa.
- **`jspDestroy`**: Similar al método `destroy` de los servlets, se llama cuando la página JSP se está destruyendo.

```jsp
<%! 
    public void jspInit() {
        System.out.println("Inicializando JSP...");
    }
    
    public void jspDestroy() {
        System.out.println("Destruyendo JSP...");
    }
%>
```

### Inhabilitar los Elementos de Scripting

Con la introducción del **Lenguaje de Expresión (EL)**, la práctica recomendada es evitar el uso de elementos de scripting en las páginas JSP para mantener una separación clara entre la lógica de negocio y la lógica de presentación. A partir de **JSP 2.0**, se pueden inhabilitar los elementos de scripting mediante el descriptor de despliegue (`web.xml`):

```xml
<jsp-property-group>
    <url-pattern>*.jsp</url-pattern>
    <scripting-invalid>true</scripting-invalid>
</jsp-property-group>
```

## Acciones JSP

Las **acciones** en JSP se traducen en código Java que realiza ciertas operaciones, como crear instancias de objetos o invocar métodos. Algunas acciones estándar incluyen:

### `jsp:useBean`

La acción **`useBean`** crea una variable de scripting asociada con un objeto Java. Es un intento temprano de separar la lógica de negocio de la presentación, aunque hoy en día su uso ha disminuido con la aparición de **EL** y **JSTL**.

```jsp
<jsp:useBean id="hoy" class="java.util.Date" />
<%= hoy %>
```

### `jsp:setProperty` y `jsp:getProperty`

- **`setProperty`**: Establece una propiedad de un objeto Java.
- **`getProperty`**: Recupera y muestra una propiedad de un objeto Java.

```jsp
<jsp:useBean id="empleado" class="com.miempresa.Empleado" />
<jsp:setProperty name="empleado" property="nombre" value="Antonio" />
Nombre: <jsp:getProperty name="empleado" property="nombre" />
```

### `jsp:include`

La acción **`include`** se usa para incluir otro recurso dinámicamente, ya sea otra página JSP, un servlet o un archivo HTML estático.

```jsp
<jsp:include page="fragmentos/menu.jsp">
    <jsp:param name="texto" value="Bienvenido" />
</jsp:include>
```

La acción `include` permite pasar parámetros, lo cual no es posible con la directiva `include`.

### `jsp:forward`

La acción **`forward`** redirige la petición a otro recurso.

```jsp
<jsp:forward page="jspf/login.jsp">
    <jsp:param name="mensaje" value="Por favor inicie sesión" />
</jsp:forward>
```

## Conclusión

Las **directivas**, **elementos de scripting** y **acciones JSP** son componentes clave para el desarrollo de páginas JSP. Sin embargo, con la llegada de **EL** y **JSTL**, es una buena práctica minimizar el uso de scripting para mantener un código limpio y enfocado únicamente en la presentación. Las páginas JSP, junto con estas características, ofrecen un poderoso mecanismo para la generación de contenido dinámico en aplicaciones Java, proporcionando la flexibilidad necesaria para manejar complejidad de una manera estructurada.

