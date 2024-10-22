# JSTL: JavaServer Pages Standard Tag Library

La **Librería de Etiquetas Estándar de JavaServer Pages (JSTL)** es un conjunto de etiquetas predefinidas que facilitan tareas comunes en el desarrollo web, como iteraciones, comprobaciones condicionales o la manipulación de datos. JSTL ayuda a reducir la cantidad de lógica Java directamente en las páginas JSP, lo cual se alinea con el paradigma moderno de desarrollo en el que se busca una separación clara entre la lógica de presentación y la lógica de negocio.

Actualmente, **JSTL** está en su versión **1.2**. Para utilizar JSTL en una aplicación web, es necesario añadir el archivo `.jar` correspondiente en el directorio `WEB-INF/lib` de la aplicación. JSTL se compone de varias librerías, siendo la **librería Core** la más utilizada.

Para utilizar JSTL en una página JSP, se debe importar la librería correspondiente mediante la directiva `taglib`:

```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
```

En este ejemplo, se está importando la librería **Core** y se está utilizando el prefijo **`c`** para acceder a sus etiquetas.

## Acciones de Propósito General

JSTL proporciona varias etiquetas para manipular variables y trabajar con diferentes ámbitos. Las tres principales son: **`out`**, **`set`** y **`remove`**.

### La Etiqueta `c:out`

La etiqueta **`c:out`** evalúa una expresión y escribe el resultado en el `JspWriter` actual, permitiendo la salida del valor al navegador. Se puede utilizar de dos formas: con o sin un valor por defecto.

```jsp
<c:out value="${x}" escapeXml="true" default="valorPorDefecto"/>
```

- **`value`**: Expresión a ser evaluada.
- **`escapeXml`**: Indica si los caracteres especiales (`<`, `>`, `&`, `'`, `"`) deben ser convertidos a sus entidades HTML correspondientes, como `&lt;` y `&gt;`. Por defecto es **`true`**.
- **`default`**: Valor que se muestra si la expresión evaluada es `null`.

Con la introducción de **JSP 2.0**, la etiqueta `c:out` fue reemplazada en parte por el uso de **EL**, ya que se puede imprimir un valor simplemente usando `${x}`.

### La Etiqueta `c:set`

La etiqueta **`c:set`** se usa para establecer el valor de una variable o propiedad de un objeto. Se puede utilizar de varias formas:

1. **Crear una nueva variable** en uno de los ámbitos (`page`, `request`, `session`, `application`):

    ```jsp
    <c:set var="miVariable" value="miValor" scope="session"/>
    ```

2. **Asignar un valor como contenido del cuerpo** de la etiqueta `set`:

    ```jsp
    <c:set var="miVariable">
        Aquí va el valor dinámico
    </c:set>
    ```

3. **Establecer la propiedad de un objeto Java** en algún ámbito:

    ```jsp
    <c:set target="${miBean}" property="nombre" value="Juan"/>
    ```

    En este ejemplo, `miBean` debe ser un JavaBean o un **`Map`**.

### La Etiqueta `c:remove`

La etiqueta **`c:remove`** se usa para eliminar una variable en uno de los ámbitos definidos (`page`, `request`, `session`, `application`). Esto elimina la referencia a la variable, pero **no destruye el objeto en memoria** si todavía existen otras referencias hacia él.

```jsp
<c:remove var="miVariable" scope="session"/>
```

## Acciones Condicionales en JSTL

Las acciones condicionales en JSTL son útiles cuando se necesita que la salida de una página JSP dependa del valor de ciertos datos. Son equivalentes a las sentencias **`if`**, **`if...else`**, y **`switch`** en Java.

### La Etiqueta `c:if`

La etiqueta **`c:if`** evalúa una condición y, si esta se cumple, procesa el contenido de su cuerpo.

```jsp
<c:if test="${miValor > 10}">
    El valor es mayor que 10.
</c:if>
```

- **`test`**: Condición que se evalúa como `true` o `false`.

### Las Etiquetas `c:choose`, `c:when` y `c:otherwise`

Las etiquetas **`c:choose`**, **`c:when`**, y **`c:otherwise`** proporcionan una estructura similar al `switch-case` de Java. Se usan para evaluar varias condiciones de forma excluyente.

```jsp
<c:choose>
    <c:when test="${status == 'activo'}">
        Usuario activo.
    </c:when>
    <c:when test="${status == 'inactivo'}">
        Usuario inactivo.
    </c:when>
    <c:otherwise>
        Estado desconocido.
    </c:otherwise>
</c:choose>
```

- **`c:when`**: Evalúa una condición. Si es verdadera, se ejecuta el bloque de código dentro del cuerpo.
- **`c:otherwise`**: Se ejecuta si ninguna de las condiciones previas es verdadera.

## Comparativa con el Paradigma Actual de Desarrollo

En el **desarrollo moderno**, el uso de **JSTL** se ha consolidado como una práctica para garantizar una clara separación de responsabilidades y evitar la mezcla de lógica de negocio con la lógica de presentación en páginas JSP. Con **JSTL** y **EL**, es posible escribir páginas JSP mucho más declarativas y legibles.

Sin embargo, en los últimos años han surgido herramientas y frameworks como **Spring Boot** con **Thymeleaf** o **React** para el frontend, que promueven una **arquitectura basada en componentes** y separan aún más la lógica del servidor y del cliente. En estas arquitecturas, la vista se maneja a través de tecnologías como **HTML dinámico** y **JavaScript**, mientras que la lógica de negocio permanece en controladores y servicios.

JSTL sigue siendo relevante cuando se trabaja con aplicaciones **Java EE** clásicas, especialmente aquellas basadas en **JSP**. Sin embargo, frameworks más modernos como **Spring MVC** y **JSF (JavaServer Faces)** han desplazado a **JSP/JSTL** hacia un papel más secundario, donde su principal ventaja radica en facilitar la migración o el mantenimiento de aplicaciones **legacy**.

En resumen, aunque **JSTL** es menos utilizado en desarrollos nuevos debido al auge de frameworks y paradigmas modernos que fomentan la **componentización** y la **API REST** en el backend, sigue siendo útil y efectivo en ciertos escenarios, especialmente en proyectos donde se utiliza **JSP** para la lógica de presentación.

# JSTL: Librería de Etiquetas Estándar de JavaServer Pages

La **Librería de Etiquetas Estándar de JavaServer Pages (JSTL)** proporciona un conjunto de etiquetas para resolver tareas comunes en el desarrollo web, como iterar sobre colecciones, realizar comprobaciones condicionales, y formatear datos. JSTL promueve una separación clara entre la lógica de presentación y la lógica de negocio, facilitando el desarrollo de páginas JSP más limpias y fáciles de mantener.

En el paradigma actual, el uso de JSTL y JSP ha disminuido con la popularidad de frameworks modernos como **Spring Boot**, **Thymeleaf**, **React**, y **Angular**, que promueven una separación más robusta entre frontend y backend mediante arquitecturas **REST** o **GraphQL**. Sin embargo, JSTL sigue siendo útil para proyectos **legacy** o aquellos basados en **Java EE**.

## Acciones de Iteración

Las acciones de iteración en JSTL son útiles para repetir un bloque de código varias veces o para iterar sobre una colección de objetos. **JSTL** proporciona dos etiquetas de iteración: **`forEach`** y **`forTokens`**.

### La Etiqueta `c:forEach`

La etiqueta **`c:forEach`** permite iterar sobre colecciones como listas, mapas o arrays. También se puede usar para repetir un bloque de código un número determinado de veces.

Los objetos sobre los que se puede iterar incluyen implementaciones de **`java.util.Collection`**, **`java.util.Map`**, arrays, y otros objetos como **`Iterator`** y **`Enumeration`**. Cabe destacar que ni **`Iterator`** ni **`Enumeration`** se reinician automáticamente después de la iteración.

**Atributos principales de `c:forEach`:**

- **`var`**: Define el nombre de la variable que referencia el elemento actual de la iteración.
- **`items`**: Colección de objetos a iterar.
- **`varStatus`**: Nombre de la variable que mantiene el estado de la iteración (tipo `LoopTagStatus`).
- **`begin`** y **`end`**: Especifican los índices de inicio y fin de la iteración.
- **`step`**: Define el incremento para cada iteración.

Ejemplos de uso de `c:forEach`:

1. **Iterar un número fijo de veces**:

    ```jsp
    <c:forEach var="i" begin="1" end="5">
        <c:out value="${i}"/>,
    </c:forEach>
    <!-- Resultado: 1, 2, 3, 4, 5, -->
    ```

2. **Iterar sobre una lista de objetos**:

    ```jsp
    <c:forEach var="telefono" items="${direccion.telefono}">
        ${telefono}<br/>
    </c:forEach>
    ```

3. **Iterar sobre un mapa**:

    ```jsp
    <c:forEach var="mapItem" items="${mapa}">
        ${mapItem.key} : ${mapItem.value}<br/>
    </c:forEach>
    ```

La etiqueta `c:forEach` también permite acceder al estado de la iteración a través del atributo **`varStatus`**. Este atributo proporciona información como la posición actual, si el elemento es el primero o el último, etc. Esto es útil, por ejemplo, para alternar estilos según la posición en la lista.

### La Etiqueta `c:forTokens`

La etiqueta **`c:forTokens`** se utiliza para iterar sobre una cadena de caracteres que contiene varios elementos delimitados por uno o más delimitadores.

**Atributos principales de `c:forTokens`:**

- **`items`**: Cadena de caracteres con los elementos separados por delimitadores.
- **`delims`**: Los delimitadores que separan los elementos dentro de la cadena.
- **`var`**: Nombre de la variable que hace referencia al elemento actual de la iteración.

Ejemplo de uso de `c:forTokens`:

```jsp
<c:forTokens var="pais" items="Argentina,Brasil,Chile" delims=",">
    <c:out value="${pais}"/><br/>
</c:forTokens>
```

Este ejemplo iterará sobre cada país de la lista separada por comas.

## Acciones de Formateado

JSTL también proporciona etiquetas para **formatear y convertir números, fechas y monedas**, lo cual es útil para aplicaciones que necesiten manejar estos datos en un formato específico dependiendo del idioma o la localización.

### La Etiqueta `fmt:formatNumber`

La etiqueta **`fmt:formatNumber`** se utiliza para formatear números, convirtiéndolos en una cadena con el formato especificado (número, moneda, porcentaje, etc.). 

**Atributos principales de `fmt:formatNumber`:**

- **`value`**: El número que se desea formatear.
- **`type`**: Define el tipo de formato (puede ser `number`, `currency` o `percent`).
- **`pattern`**: Permite especificar un patrón de formato personalizado.
- **`currencyCode`**: Código de la moneda según el estándar ISO 4217 (e.g., `USD`, `EUR`).

Ejemplos de uso de `fmt:formatNumber`:

1. **Formatear como moneda**:

    ```jsp
    <fmt:formatNumber value="12345.67" type="currency" currencyCode="USD"/>
    <!-- Resultado: $12,345.67 -->
    ```

2. **Formatear como porcentaje**:

    ```jsp
    <fmt:formatNumber value="0.85" type="percent" minFractionDigits="1"/>
    <!-- Resultado: 85.0% -->
    ```

### La Etiqueta `fmt:formatDate`

La etiqueta **`fmt:formatDate`** se utiliza para formatear fechas y horas.

**Atributos principales de `fmt:formatDate`:**

- **`value`**: Fecha u hora que se desea formatear.
- **`type`**: Tipo de formato (`date`, `time` o `both`).
- **`dateStyle`** y **`timeStyle`**: Definen el estilo (`short`, `medium`, `long`, `full`).
- **`timeZone`**: Permite especificar la zona horaria.

Ejemplos de uso de `fmt:formatDate`:

```jsp
<fmt:formatDate value="${now}" type="both" dateStyle="full" timeStyle="short"/>
<!-- Resultado: Tuesday, October 24, 2023 10:45 AM -->
```

## Comparativa con el Paradigma Actual de Desarrollo

En el **paradigma moderno de desarrollo**, las etiquetas JSTL de iteración y formateo son comparables a las directivas y funciones usadas en frameworks como **React** o **Angular**, donde se usan bucles y componentes de manera declarativa para iterar y mostrar datos. La lógica de iteración y el formateo a menudo se delegan al lenguaje del cliente (JavaScript) con frameworks como **Lodash** o utilizando funcionalidades nativas como **map()** y **filter()**.

Además, en las aplicaciones modernas, el **formateo de números y fechas** suele hacerse del lado del cliente para mejorar la experiencia de usuario, usando librerías como **moment.js** o **date-fns** en JavaScript. Esto se debe a que manejar estos aspectos en el cliente permite una respuesta más ágil sin necesidad de realizar constantes llamadas al servidor.

En aplicaciones basadas en **Spring Boot** y **Thymeleaf**, se tiende a utilizar funciones de formateo dentro de plantillas Thymeleaf, mientras que la lógica de iteración y formateo se escribe directamente en el código del controlador o servicio. Esto permite una **separación de responsabilidades más clara** y una lógica de presentación más flexible.

Por tanto, aunque JSTL proporciona una forma sólida de manejar iteraciones y formateo en JSP, los frameworks modernos ofrecen soluciones más avanzadas que permiten mantener el **frontend** y el **backend** lo más desacoplados posible, promoviendo la reutilización de componentes y una mejor **experiencia de desarrollo**.

### La Etiqueta `timeZone`

La etiqueta `timeZone` se usa para especificar la zona horaria en la cual la información horaria contenida en su cuerpo debe ser formateada o analizada. Esta etiqueta es útil en aplicaciones que manejan usuarios de diferentes zonas horarias, asegurando que los datos de tiempo se ajusten adecuadamente según la ubicación del usuario.

```jsp
<fmt:timeZone value="timeZone">
    body content
</fmt:timeZone>
```

El contenido del cuerpo es JSP. Al atributo `value` se le puede pasar un valor dinámico de tipo `String` o `java.util.TimeZone`. Si el atributo `value` es `null` o vacío, se usará la zona horaria GMT por defecto.

**Ejemplo de uso:**

```jsp
<fmt:timeZone value="GMT+1:00">
    <fmt:formatDate value="${now}" type="both" dateStyle="full" timeStyle="full"/>
</fmt:timeZone>
```

### Comparación con el Paradigma Moderno

Actualmente, muchas aplicaciones web manejan zonas horarias y ajustes de localización de una forma más automatizada mediante el uso de APIs modernas como JavaScript `Intl.DateTimeFormat` en el lado del cliente o librerías en el servidor como `Moment.js`, `luxon` o incluso características avanzadas de frameworks como Spring Boot. Estas herramientas permiten manejar zonas horarias de manera mucho más flexible y con menos complejidad en el código.

### La Etiqueta `setTimeZone`

La etiqueta `setTimeZone` se usa para almacenar la zona horaria especificada en una variable o configurar la zona horaria de una aplicación JSP. Es útil cuando se necesita utilizar la misma zona horaria en múltiples partes de una aplicación.

```jsp
<fmt:setTimeZone value="timeZone" [var="varName"] [scope="{page|request|session|application}"] />
```

**Atributos:**
- `value`: `String` o `java.util.TimeZone`. Define la zona horaria a usar.
- `var`: `String`. Nombre de la variable donde se almacenará la zona horaria.
- `scope`: `String`. Define el ámbito de la variable (`page`, `request`, `session`, `application`).

### Comparación con el Paradigma Moderno

En el desarrollo moderno, se suele configurar la zona horaria a nivel de base de datos o en las configuraciones del framework de backend. Los frameworks modernos permiten especificar las zonas horarias para todos los usuarios por configuración, evitando así el manejo manual de cada instancia.

### La Etiqueta `parseNumber`

La etiqueta `parseNumber` se usa para analizar una representación en forma de cadena de un número, una moneda, o un porcentaje en formato sensible al lenguaje y convertirlo a un número. Esto resulta útil en la internacionalización de aplicaciones donde los formatos de número y moneda cambian según la localización.

**Sintaxis:**

```jsp
<fmt:parseNumber value="numericValue" [type="{number|currency|percent}"] [pattern="customPattern"] [parseLocale="parseLocale"] [integerOnly="{true|false}"] [var="varName"] [scope="{page|request|session|application}"] />
```

**Ejemplo:**

```jsp
<fmt:parseNumber var="formattedNumber" type="number" value="${quantity}"/>
```

### Comparación con el Paradigma Moderno

Actualmente, el análisis de números y formatos monetarios suele hacerse con herramientas más avanzadas y flexibles, como las proporcionadas por la API de internacionalización de JavaScript (Intl). En el lado del backend, frameworks como Spring Boot proporcionan características de binding que automáticamente convierten valores de formulario al tipo de dato correcto según la localización del usuario.

### La Etiqueta `parseDate`

La etiqueta `parseDate` analiza una representación en forma de cadena de caracteres de una fecha y hora en un formato sensible al lenguaje. Esto facilita la conversión de cadenas de caracteres que representan fechas en objetos `Date` de Java.

**Sintaxis:**

```jsp
<fmt:parseDate value="dateString" [type="{time|date|both}"] [dateStyle="{default|short|medium|long|full}"] [timeStyle="{default|short|medium|long|full}"] [pattern="customPattern"] [timeZone="timeZone"] [parseLocale="parseLocale"] [var="varName"] [scope="{page|request|session|application}"] />
```

**Ejemplo:**

```jsp
<c:set var="myDate" value="12/12/2005"/>
<fmt:parseDate var="formattedDate" type="date" dateStyle="short" value="${myDate}"/>
```

### Comparación con el Paradigma Moderno

Hoy en día, la manipulación y análisis de fechas en aplicaciones web suele realizarse utilizando librerías robustas como `java.time` en Java 8 y versiones posteriores, o mediante APIs de JavaScript en el lado del cliente. Estas librerías proporcionan una forma más segura y menos propensa a errores de manipular fechas y horarios, además de facilitar el manejo de diferentes zonas horarias de forma transparente y sin necesidad de definir configuraciones explícitas en cada página JSP.
