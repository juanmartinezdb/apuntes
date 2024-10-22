# Interfaz ServletContext

La interfaz **ServletContext** representa la aplicación servlet en su totalidad. Solo existe una instancia de `ServletContext` por cada aplicación web. En un entorno distribuido, donde la aplicación se despliega simultáneamente en varios contenedores o servidores, hay un objeto `ServletContext` por cada Máquina Virtual Java (JVM).

El `ServletContext` se puede obtener llamando al método `getServletContext` del objeto **ServletConfig**. Este contexto se utiliza principalmente para compartir información entre los diferentes componentes de la aplicación, como los servlets, las páginas JSP, y otros recursos. Además, también permite el registro dinámico de objetos web durante la ejecución de la aplicación.

Para compartir información entre los recursos, el `ServletContext` mantiene un **mapa interno** en el que se almacenan los atributos. Estos atributos son objetos que pueden ser accedidos por cualquier servlet dentro de la aplicación.

Los métodos que se usan para gestionar estos atributos son los siguientes:

- `Object getAttribute(String name)`: Obtiene el valor del atributo con el nombre especificado.
- `Enumeration<String> getAttributeNames()`: Devuelve los nombres de todos los atributos almacenados.
- `void setAttribute(String name, Object object)`: Establece un nuevo atributo o actualiza uno existente.
- `void removeAttribute(String name)`: Elimina un atributo del contexto.

## Clase GenericServlet

**GenericServlet** es una clase abstracta que proporciona una implementación básica de las interfaces **Servlet** y **ServletConfig**, simplificando así el desarrollo de servlets. Esta clase es útil cuando se desarrollan servlets que no están específicamente ligados al protocolo HTTP.

Las principales tareas realizadas por `GenericServlet` son:

- Asignar el objeto **ServletConfig** en el método `init` a un atributo de instancia, de modo que pueda ser recuperado llamando al método `getServletConfig`.
- Proporcionar implementaciones por defecto para todos los métodos de la interfaz **Servlet**, lo que permite al desarrollador enfocarse solo en la funcionalidad relevante.
- Proporcionar métodos que encapsulan los métodos de la interfaz `ServletConfig`.

`GenericServlet` almacena el objeto `ServletConfig` asignándolo a un atributo de instancia `servletConfig` en el método `init`. Si un servlet sobreescribe este método, es importante llamar a `super.init(servletConfig)` para garantizar que el objeto `ServletConfig` se asigne correctamente.

Además, `GenericServlet` proporciona un segundo método `init` sin parámetros, que es llamado por el primer método `init` después de que el `ServletConfig` ha sido asignado al atributo:

```java
public void init(ServletConfig servletConfig) throws ServletException {
    this.servletConfig = servletConfig;
    this.init();
}
```

Esto significa que se puede escribir código de inicialización sobreescribiendo el método `init` sin parámetros, y el `ServletConfig` se gestionará automáticamente.

Aunque `GenericServlet` fue un gran avance con respecto a la implementación manual de **Servlet**, en la actualidad su uso es bastante limitado, ya que la mayoría de las aplicaciones trabajan sobre **HTTP**, lo que hace que la clase **HttpServlet** sea una mejor opción.

## HTTP Servlets

La mayoría de las aplicaciones web desarrolladas con servlets utilizan el protocolo **HTTP**, y para facilitar el trabajo con HTTP, se utiliza la clase **HttpServlet**. `HttpServlet` extiende `GenericServlet` y proporciona una implementación adaptada para trabajar específicamente con las características del protocolo HTTP.

Cuando se utiliza `HttpServlet`, se trabaja con los objetos **HttpServletRequest** y **HttpServletResponse**, que representan la petición y la respuesta respectivamente. La interfaz `HttpServletRequest` extiende `ServletRequest`, mientras que `HttpServletResponse` extiende `ServletResponse`. Esto permite que `HttpServlet` trabaje de forma más adecuada con las características de HTTP, como los métodos GET y POST, las cabeceras HTTP, las cookies, y más.

`HttpServlet` sobreescribe el método `service` de `GenericServlet` y añade un nuevo método `service` con la siguiente especificación:

```java
protected void service(HttpServletRequest request, HttpServletResponse response) 
    throws ServletException, IOException
```

La diferencia principal entre el nuevo método `service` y el de la interfaz `Servlet` es que el primero acepta objetos `HttpServletRequest` y `HttpServletResponse` en lugar de `ServletRequest` y `ServletResponse`. Esto permite trabajar directamente con la funcionalidad específica de HTTP.

El contenedor de servlets siempre llama al método `service` original, que en `HttpServlet` está implementado de la siguiente manera:

```java
public void service(ServletRequest req, ServletResponse res) 
    throws ServletException, IOException {
    HttpServletRequest request;
    HttpServletResponse response;
    try {
        request = (HttpServletRequest) req;
        response = (HttpServletResponse) res;
    } catch (ClassCastException e) {
        throw new ServletException("Non-HTTP request or response");
    }
    service(request, response);
}
```

Esta conversión explícita es segura, ya que el contenedor siempre pasa instancias de `HttpServletRequest` y `HttpServletResponse` al método `service`.

Una vez convertida la petición, el nuevo método `service` examina el método HTTP usado para enviar la solicitud (llamando a `request.getMethod()`) y llama a uno de los siguientes métodos:

- **doGet**
- **doPost**
- **doHead**
- **doPut**
- **doTrace**
- **doOptions**
- **doDelete**

Cada uno de estos métodos representa un método del protocolo HTTP, siendo `doGet` y `doPost` los más comunes. Normalmente, no se sobreescribe el método `service`, sino que se sobreescriben `doGet` o `doPost` (o ambos) para proporcionar la lógica de la aplicación.

### Características de HttpServlet

Hay dos características clave en `HttpServlet` que no se encuentran en `GenericServlet`:

1. En lugar de sobreescribir el método `service`, se suele sobreescribir `doGet`, `doPost` u otros métodos HTTP según la necesidad.
2. Trabaja específicamente con `HttpServletRequest` y `HttpServletResponse`, lo cual permite acceder a funcionalidades avanzadas de HTTP como manejo de cabeceras, cookies y sesiones.

## Interfaz HttpServletRequest

La interfaz **HttpServletRequest** representa la petición HTTP al servlet. Esta interfaz extiende `ServletRequest` y añade varios métodos adicionales que permiten trabajar con las particularidades de HTTP. Algunos de los métodos más importantes son:

- **String getContextPath()**: Devuelve la parte de la URI que indica el contexto de la aplicación.
- **Cookie[] getCookies()**: Devuelve una matriz de objetos **Cookie** que representa las cookies enviadas por el cliente.
- **String getHeader(String name)**: Devuelve el valor de una cabecera HTTP específica.
- **String getMethod()**: Devuelve el método HTTP utilizado en la petición (GET, POST, etc.).
- **String getQueryString()**: Devuelve la cadena de consulta de la URL, si existe.
- **HttpSession getSession()**: Devuelve el objeto **HttpSession** asociado con la petición. Si no existe, se crea uno nuevo.
- **HttpSession getSession(boolean create)**: Similar al anterior, pero permite especificar si se debe crear una nueva sesión si no existe una.

## Interfaz HttpServletResponse

La interfaz **HttpServletResponse** representa la respuesta que se envía al cliente. Algunos de los métodos importantes de esta interfaz son:

- **void addCookie(Cookie cookie)**: Añade una cookie a la respuesta.
- **void addHeader(String name, String value)**: Añade una cabecera HTTP a la respuesta.
- **void sendRedirect(String location)**: Envía un código de redirección que indica al navegador que debe realizar una nueva solicitud a la ubicación especificada.

Estas interfaces permiten trabajar de forma avanzada con las características del protocolo HTTP, proporcionando un control detallado sobre la comunicación entre el cliente y el servidor.
