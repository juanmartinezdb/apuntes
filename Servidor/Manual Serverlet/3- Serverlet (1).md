# Servlets

Los **Servlets** son la tecnología principal para el desarrollo de aplicaciones web en Java. Un **servlet** es una interfaz que todas las clases servlet deben implementar, ya sea de manera directa o indirecta. Esta interfaz define un contrato entre un servlet y el contenedor de servlets, lo que significa que el contenedor promete cargar en memoria la clase del servlet y llamar a ciertos métodos específicos durante el ciclo de vida de la instancia del servlet.

Una de las características fundamentales de los servlets es que solo puede existir una instancia de cada tipo de servlet en una aplicación. Cuando un usuario realiza una petición, el contenedor de servlets invoca el método `service` del servlet correspondiente, pasándole una instancia de **ServletRequest** y **ServletResponse**. Estas instancias permiten manejar las solicitudes y respuestas HTTP sin necesidad de manipular directamente los datos de bajo nivel.

- **ServletRequest** encapsula la petición HTTP actual y permite acceder a parámetros, cabeceras y otra información relevante de la solicitud, facilitando el manejo de datos sin tener que preocuparse de los detalles de bajo nivel.
- **ServletResponse** representa la respuesta HTTP que el servidor envía al cliente, permitiendo construir la respuesta de una manera eficiente.

Para cada aplicación, el contenedor de servlets también crea una instancia de **ServletContext**, que encapsula los detalles del entorno del contexto de la aplicación. Solo existe un `ServletContext` por cada contexto, y para cada instancia de servlet, hay un **ServletConfig** que encapsula la configuración del servlet.

## Interfaz Servlet

La interfaz **Servlet** define cinco métodos esenciales:

- `void init(ServletConfig config) throws ServletException;`
- `void service(ServletRequest request, ServletResponse response) throws ServletException, IOException;`
- `void destroy();`
- `String getServletInfo();`
- `ServletConfig getServletConfig();`

Los métodos `init`, `service`, y `destroy` se conocen como métodos de **ciclo de vida**, y el contenedor de servlets los invoca siguiendo ciertas reglas:

- **init**: Este método es invocado la primera vez que se hace una petición al servlet. Se utiliza para realizar cualquier inicialización necesaria. Por ejemplo, cargar configuraciones o inicializar conexiones. El contenedor de servlets le pasa un objeto `ServletConfig` al método `init`, que típicamente se almacena para ser usado en otras partes del servlet.

- **service**: Este es el método principal que se ejecuta cada vez que llega una nueva petición para el servlet. Aquí es donde reside el código que proporciona la funcionalidad del servlet. Dependiendo del método HTTP (`GET`, `POST`, etc.), se maneja la solicitud de manera específica.

- **destroy**: Este método es invocado cuando el servlet va a ser destruido, ya sea porque la aplicación se está desinstalando o porque el contenedor de servlets se está apagando. Normalmente, en este método se liberan recursos, se cierran conexiones y se realizan tareas de limpieza.

Los otros dos métodos (`getServletInfo` y `getServletConfig`) son métodos estándar:

- **getServletInfo**: Devuelve una descripción del servlet. Esto puede ser cualquier información útil o incluso `null`.
- **getServletConfig**: Devuelve el objeto `ServletConfig` que fue pasado al método `init`.

Una instancia de un servlet es compartida por todos los usuarios de la aplicación, por lo que no es recomendable tener atributos de instancia que puedan ser modificados, ya que esto podría causar problemas de concurrencia y datos inconsistentes.

## Configuración Básica de un Servlet

La forma más sencilla de configurar un servlet en aplicaciones modernas es mediante **anotaciones**. La anotación **@WebServlet** a nivel de clase se usa para declarar un servlet:

```java
@WebServlet(name = "MiServlet", urlPatterns = {"/miServlet"})
public class MiServlet extends HttpServlet {
    // Implementación del servlet
}
```

- **name**: Es un atributo opcional que permite nombrar al servlet.
- **urlPatterns**: Define los patrones de URL que deben invocar al servlet. Este atributo es común y siempre debe comenzar con una barra inclinada (`/`).

El uso de anotaciones simplifica la configuración, eliminando la necesidad de modificar archivos de configuración como `web.xml`.

## Estructura de Directorios de la Aplicación

Una aplicación servlet debe ser desplegada con una estructura de directorios específica. El directorio base es el **directorio de la aplicación**, y dentro de este se encuentra el directorio **WEB-INF**, que tiene dos subdirectorios importantes:

1. **classes**: Contiene las clases compiladas del servlet y otras clases Java necesarias. La estructura de directorios dentro de `classes` refleja la estructura de paquetes de las clases.
2. **lib**: Almacena los ficheros JAR necesarios para la aplicación, como dependencias externas.

Una aplicación servlet/JSP normalmente contiene **páginas JSP**, **archivos HTML**, **imágenes** y otros recursos que se organizan en subdirectorios bajo el directorio principal de la aplicación. Cualquier recurso colocado directamente bajo el directorio de la aplicación es accesible directamente desde el navegador, mientras que los recursos colocados bajo `WEB-INF` no son accesibles desde el navegador directamente y están protegidos, siendo solo accesibles para los servlets.

El método recomendado para desplegar una aplicación servlet/JSP es crear un **archivo WAR (Web Application Archive)**, que es básicamente un archivo JAR con la extensión `.war`. Este archivo puede crearse de diferentes maneras, como usando la herramienta **jar** que viene con el JDK de Java, con herramientas de compresión como **WinZip**, o con herramientas de construcción y automatización como **Ant** o **Maven**.

## Interfaz ServletRequest

Cada vez que se realiza una petición HTTP, el contenedor de servlets crea una instancia de la interfaz **ServletRequest** y la pasa al método `service` del servlet. **ServletRequest** encapsula la información relacionada con la solicitud, permitiendo acceder a parámetros, cabeceras, y más.

El método más utilizado de `ServletRequest` es **getParameter**, que se utiliza para obtener el valor de un campo de formulario HTML. También se puede usar para recuperar valores de parámetros de una cadena de consulta (`query string`). Es importante tener en cuenta que `getParameter` devuelve `null` si el parámetro solicitado no existe.

Además de `getParameter`, existen otros métodos útiles:

- **getParameterNames**: Devuelve una enumeración con los nombres de todos los parámetros.
- **getParameterMap**: Devuelve un mapa con los pares nombre-valor de los parámetros.
- **getParameterValues**: Devuelve todos los valores de un parámetro si tiene múltiples valores.

## Interfaz ServletResponse

La interfaz **ServletResponse** representa la respuesta de un servlet. Antes de invocar al método `service`, el contenedor de servlets crea una instancia de `ServletResponse` y la pasa como segundo argumento al método. **ServletResponse** oculta la complejidad de enviar una respuesta al navegador.

Uno de los métodos más utilizados en `ServletResponse` es **getWriter**, que devuelve un objeto `java.io.PrintWriter` que se utiliza para enviar texto al cliente. Generalmente, el contenido de la respuesta es **HTML**, y antes de enviar cualquier etiqueta, se debe establecer el tipo de contenido llamando al método **setContentType**, pasándole `"text/html"` como argumento. De esta forma se informa al navegador que el contenido es HTML.

## Interfaz ServletConfig

El contenedor de servlets pasa una instancia de la interfaz **ServletConfig** al método `init` cuando inicializa el servlet. **ServletConfig** encapsula información de configuración que puede ser pasada al servlet a través de la anotación **@WebServlet** o mediante un descriptor de despliegue (`web.xml`). Esta información se denomina **parámetro inicial**, y cada parámetro tiene una clave y un valor.

Para recuperar el valor de un parámetro inicial desde el servlet, se utiliza el método **getInitParameter** en la instancia `ServletConfig`:

```java
String valor = config.getInitParameter("miParametro");
```

Además, el método **getInitParameterNames** devuelve una enumeración con todos los nombres de los parámetros iniciales:

```java
Enumeration<String> nombres = config.getInitParameterNames();
```

Otro método importante en `ServletConfig` es **getServletContext**, que permite obtener la instancia de `ServletContext` desde el servlet y acceder a información global de la aplicación.

