# Trabajar con Formularios HTML en Servlets

Una aplicación web casi siempre contiene uno o más formularios HTML para recoger entradas del usuario. En el contexto de los **servlets**, estos formularios se utilizan para recopilar información y enviarla al servidor, que puede ser procesada y utilizada para interactuar con el sistema.

Cuando el usuario envía un formulario HTML, los valores introducidos en los elementos del formulario se envían al servidor como **parámetros de la petición**. Estos valores se envían en forma de cadenas de caracteres, y cada tipo de elemento del formulario se maneja de manera diferente:

- **Campos de texto, campos ocultos y campos de contraseña**: Estos envían una cadena de caracteres con el valor ingresado. Si el campo está vacío, se envía una cadena vacía (`""`). Esto significa que el método `ServletRequest.getParameter(String name)` nunca devuelve `null` para estos tipos de campos, sino una cadena vacía si el valor está vacío.

- **Elementos de selección**: Un `<select>` en un formulario envía el valor de la opción seleccionada. Si se trata de un elemento de selección múltiple (`<select multiple>`), se utiliza el método `ServletRequest.getParameterValues(String name)` para obtener una matriz de los valores seleccionados.

- **Checkboxes**: Un checkbox marcado envía la cadena `"on"` al servidor, mientras que un checkbox no marcado no envía nada. En este caso, `ServletRequest.getParameter(fieldName)` devolverá `null` si el checkbox no está marcado.

- **Radio buttons**: Un radio button envía el valor del botón seleccionado. Si no se selecciona ningún radio button, no se envía nada y `getParameter(fieldName)` devuelve `null`.

Si el formulario contiene **múltiples elementos de entrada con el mismo nombre**, todos los valores serán enviados y se deben recuperar usando `getParameterValues`. `getParameter` solo devolverá el valor del último elemento.

## Uso del Descriptor de Despliegue (`web.xml`)

Además de las anotaciones como **@WebServlet**, la configuración de los servlets y otras características de la aplicación se pueden definir utilizando un **descriptor de despliegue**. Este archivo siempre se llama `web.xml` y se encuentra bajo el directorio **WEB-INF** de la aplicación.

El descriptor de despliegue tiene varias ventajas sobre el uso de anotaciones:

- Permite elementos de configuración que no tienen equivalente en las anotaciones, como el elemento **`<load-on-startup>`**, que permite cargar el servlet en el momento en que la aplicación arranca, en lugar de la primera vez que se invoca. Esto es útil para inicializar servlets que requieran una configuración larga.

- **Sobreescritura de configuraciones**: Un servlet declarado tanto con anotación como en el descriptor de despliegue se regirá por la configuración del descriptor, ignorando la anotación. Esto permite mayor flexibilidad y control sobre el comportamiento de los servlets.

### Ejemplo de Descriptor de Despliegue (`web.xml`)

```xml
<web-app>
    <servlet>
        <servlet-name>MiServlet</servlet-name>
        <servlet-class>com.miempresa.MiServlet</servlet-class>
        <load-on-startup>1</load-on-startup>
    </servlet>
    
    <servlet-mapping>
        <servlet-name>MiServlet</servlet-name>
        <url-pattern>/miServlet</url-pattern>
    </servlet-mapping>
</web-app>
```

En este ejemplo, el servlet se carga al inicio (`<load-on-startup>`), y se mapea a la ruta `/miServlet`.

## Gestión de Sesión en Servlets

La gestión de sesión es esencial en el desarrollo de aplicaciones web, ya que **HTTP es un protocolo sin estado**. Esto significa que cada petición HTTP es independiente y el servidor no tiene forma de saber si las peticiones sucesivas provienen del mismo usuario.

Por ejemplo, si un usuario se registra correctamente, la aplicación necesita recordar este hecho para no requerir que el usuario se registre en cada página. Esto se logra mediante la **gestión de sesiones**.

### Objetos HttpSession

Los objetos **HttpSession** son una de las técnicas más poderosas y versátiles para la gestión de sesiones. Cada usuario tiene una única instancia de `HttpSession`, y solo puede acceder a su propia sesión. Un objeto `HttpSession` se crea automáticamente la primera vez que un usuario visita la página.

Se puede recuperar el objeto `HttpSession` llamando al método **`getSession`** del objeto `HttpServletRequest`:

- **`HttpSession getSession()`**: Devuelve la sesión actual, o crea una nueva si no existe ninguna.
- **`HttpSession getSession(boolean create)`**: Si `create` es `true`, se crea una nueva sesión si no existe; si `false`, se devuelve la sesión actual o `null` si no existe.

Una vez que se tiene un objeto `HttpSession`, se pueden almacenar atributos utilizando **`setAttribute(String name, Object value)`**. Estos atributos se almacenan en memoria y pueden ser cualquier objeto Java, siempre que implementen la interfaz **Serializable** si es necesario serializarlos.

### Ejemplo de Uso de HttpSession

```java
HttpSession session = request.getSession();
session.setAttribute("usuario", usuarioLogueado);
Usuario usuario = (Usuario) session.getAttribute("usuario");
```

En este ejemplo, se almacena un objeto `usuarioLogueado` en la sesión y luego se recupera en una solicitud posterior.

### Consideraciones sobre el Uso de Sesiones

- Los valores almacenados en la sesión **no se envían al cliente**. En su lugar, el contenedor genera un **identificador de sesión único** (normalmente `JSESSIONID`), que se envía al navegador en forma de **cookie** o se añade a las URLs como parámetro `jsessionid`.
- Se puede recuperar el identificador de la sesión llamando al método **`getId()`** del objeto `HttpSession`.
- Para forzar la expiración de una sesión y liberar todos los recursos asociados, se puede utilizar el método **`invalidate()`**. Esto es útil para cerrar la sesión de un usuario de forma controlada.
- El tiempo de expiración de una sesión puede configurarse a nivel de aplicación mediante el elemento **`<session-timeout>`** en `web.xml`, o de manera individual mediante el método **`setMaxInactiveInterval(int seconds)`** de `HttpSession`.

## Ejemplo de Configuración de Expiración de Sesiones en `web.xml`

```xml
<session-config>
    <session-timeout>30</session-timeout> <!-- 30 minutos de inactividad -->
</session-config>
```

Este fragmento configura un tiempo de expiración de 30 minutos para todas las sesiones de la aplicación.

## Buenas Prácticas para la Gestión de Sesiones

- **Minimizar el tamaño de los objetos en sesión**: Los objetos almacenados en la sesión deben ser lo más pequeños posible, ya que el almacenamiento en la memoria puede afectar al rendimiento del servidor.
- **Evitar que la sesión nunca expire** (`setMaxInactiveInterval(0)`) salvo que sea absolutamente necesario, ya que esto puede llevar a problemas de memoria y rendimiento.
- **Cerrar las sesiones cuando ya no sean necesarias** utilizando `invalidate()` para liberar los recursos ocupados.

## Conclusión

Trabajar con **formularios HTML**, el **descriptor de despliegue** y la **gestión de sesiones** son aspectos fundamentales en el desarrollo de aplicaciones con servlets. Utilizar adecuadamente `HttpSession` permite mantener el estado del usuario de manera efectiva, mientras que el descriptor `web.xml` proporciona una mayor flexibilidad en la configuración de los servlets. Mantener estas prácticas actualizadas en el contexto de desarrollo moderno garantiza aplicaciones robustas, escalables y fáciles de mantener.
