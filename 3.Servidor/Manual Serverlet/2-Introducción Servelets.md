# Introducción a Servlets

La tecnología Servlet de Java es la base para desarrollar aplicaciones web en Java. Lanzada en 1996, fue creada para competir con las aplicaciones CGI, que en ese momento eran el estándar para generar contenido dinámico en la web. El principal problema con las aplicaciones CGI era que arrancaban un nuevo proceso por cada nueva petición HTTP, lo cual resultaba ineficiente. Un servlet, por el contrario, es un mecanismo mucho más rápido, ya que permanece en memoria después de atender la primera petición, esperando subsiguientes solicitudes.

Los **servlets** son clases Java que se ejecutan en un contenedor de servlets. Un contenedor de servlets o motor de servlets es un servidor web que tiene la capacidad de generar contenido dinámico, no solo servir recursos estáticos. Ejemplos de estos contenedores son **Apache Tomcat** y **Jetty**, que son de los más populares y, además, son gratuitos y de código abierto.

## Arquitectura de Aplicación Servlet/JSP

Un servlet es básicamente un programa Java. Una aplicación servlet puede contener uno o más servlets, y las páginas **JSP (JavaServer Pages)** se traducen y compilan a servlets para poder ser ejecutadas. Es decir, cada página JSP es transformada internamente a un servlet.

Una aplicación servlet se ejecuta en un contenedor de servlets y no puede ejecutarse de manera autónoma. El contenedor es el encargado de gestionar las peticiones de los usuarios, pasando las solicitudes al servlet correspondiente y devolviendo las respuestas al usuario final.

Los usuarios utilizan navegadores web para acceder a las aplicaciones servlet, y estos navegadores se denominan **clientes web**. La comunicación entre el servidor web y el cliente web se realiza mediante un protocolo común: el **Protocolo de Transferencia de Hipertexto (HTTP)**.

Un **contenedor servlet/JSP** es un servidor web especializado que puede procesar tanto servlets como contenido estático. Algunos ejemplos conocidos de estos contenedores son **Apache Tomcat** y **Jetty**. Estos contenedores, aunque potentes, no cumplen con toda la especificación de **Java EE** y, por tanto, no pueden ejecutar componentes como **Enterprise JavaBeans (EJB)** o **Java Message Service (JMS)**. En contraste, otros servidores de aplicaciones más completos, como **GlassFish**, **JBoss**, **Oracle WebLogic** o **IBM WebSphere**, sí permiten ejecutar estos componentes y ofrecen toda la funcionalidad de Java EE, aunque también son más pesados.

## Protocolo HTTP (Hypertext Transfer Protocol)

El protocolo **HTTP** permite a los servidores y navegadores web intercambiar datos sobre Internet o una intranet. Un servidor web permanece en ejecución esperando a que los clientes web se conecten a él para pedir recursos. En HTTP, siempre es el cliente quien inicia la conexión, mientras que el servidor responde. Para localizar recursos, se usan **URLs (Uniform Resource Locator)**, por ejemplo: `http://google.com/index.html`.

Una URL generalmente tiene el siguiente formato:

```
protocolo://[host.]dominio[:puerto[/contexto][/recurso][?cadena consulta]
```

O bien:

```
protocolo://direccion IP[:puerto[/contexto][/recurso][?cadena consulta]
```

- **Protocolo**: Especifica el protocolo utilizado (HTTP, HTTPS, FTP, etc.).
- **Host**: Puede identificar ubicaciones específicas en Internet (ej. www).
- **Dominio**: El nombre de la máquina o dominio del servidor.
- **Puerto**: Identifica el puerto del servidor. Si es el puerto 80 (por defecto para HTTP), se omite en la URL.
- **Contexto**: Corresponde al nombre de la aplicación.
- **Recurso**: Representa el archivo o página que se solicita.

Por ejemplo, `http://localhost:8080` indica que el navegador debe conectarse al servidor que está ejecutándose en la máquina local (`localhost`), en el puerto 8080.

## Peticiones HTTP

Una petición HTTP consta de tres partes principales:

1. **Línea de solicitud**: Contiene el método, el URI y la versión del protocolo.
2. **Cabeceras de la petición**: Incluyen información sobre el cliente, el formato aceptado, entre otros.
3. **Cuerpo de la petición**: Opcional, puede contener datos adicionales que se envían al servidor.

Un ejemplo de una petición HTTP es la siguiente:

```
POST /examples/default.jsp HTTP/1.1
Accept: text/plain; text/html
Accept-Language: en-gb
Connection: Keep-Alive
Host: localhost
User-Agent: Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9)
Content-Length: 30
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip, deflate

lastName=Blanks&firstName=Mike
```

En la primera línea se especifica el **método de la petición** (`POST`), el **URI** (`/examples/default.jsp`), y el **protocolo/versión** (`HTTP/1.1`). HTTP soporta varios métodos, entre los cuales los más comunes en aplicaciones web son **GET** y **POST**.

- **GET**: Se utiliza para solicitar datos del servidor.
- **POST**: Se utiliza para enviar datos al servidor, normalmente desde un formulario.

Las **cabeceras de la petición** incluyen detalles como el tipo de contenido aceptado (`Accept`), el idioma (`Accept-Language`), y la longitud del contenido (`Content-Length`), entre otros.

El **cuerpo de la petición**, si existe, contiene los datos que se están enviando al servidor. En el ejemplo, se envían los valores `lastName=Blanks` y `firstName=Mike`.

## Respuestas HTTP

Una respuesta HTTP, al igual que una petición, consta de tres partes:

1. **Línea de estado**: Contiene el protocolo, el código de estado y una descripción.
2. **Cabeceras de la respuesta**: Proporcionan información sobre la respuesta, similar a las cabeceras de la petición.
3. **Cuerpo**: Contiene el recurso solicitado.

Un ejemplo de una respuesta HTTP es la siguiente:

```
HTTP/1.1 200 OK
Server: Apache-Coyote/1.1
Date: Thu, 5 Jan 2012 13:13:33 GMT
Last-Modified: Wed, 4 Jan 2012 13:13:12 GMT
Content-Length: 30

<html>
<head>
<title>Ejemplo Respuesta HTTP</title>
</head>
<body>
Hola como estamos
</body>
</html>
```

La primera línea de la respuesta indica el **protocolo** (`HTTP/1.1`), el **código de estado** (`200` significa éxito) y una breve **descripción** (`OK`). Existen otros códigos de estado para diferentes situaciones, como **404** (recurso no encontrado) o **401** (acceso no autorizado).

Las **cabeceras de la respuesta** proporcionan información similar a las cabeceras de la petición, mientras que el **cuerpo de la respuesta** contiene el contenido solicitado, generalmente en formato **HTML**.

## Resumen

La tecnología de **Servlets** y **JSP** de Java sigue siendo fundamental para el desarrollo de aplicaciones web en Java. Entender la comunicación mediante **HTTP** y cómo los contenedores de servlets gestionan peticiones y respuestas es crucial para trabajar eficientemente con estas tecnologías. En el próximo capítulo, podemos explorar en detalle la creación y configuración de un servlet básico y cómo interactúa con la capa de presentación.
