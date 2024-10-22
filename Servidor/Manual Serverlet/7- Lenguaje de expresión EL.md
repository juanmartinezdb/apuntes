# Lenguaje de Expresión EL (Expression Language)

El **Lenguaje de Expresión (EL)** facilita el acceso a los datos de una aplicación desde las páginas JSP, y está diseñado para fomentar la creación de páginas **JSP sin scripts**, es decir, sin declaraciones, expresiones o scriptlets. Con EL, se puede lograr una separación clara entre la lógica de negocio y la lógica de presentación, alineándose con las prácticas modernas de desarrollo que buscan mantener el código más legible y mantener los aspectos de lógica lejos de la vista.

## Sintaxis del Lenguaje de Expresión

Las expresiones en EL comienzan con `${` y terminan con `}`. La sintaxis básica es:

```jsp
${expresión}
```

El carácter `${` denota el inicio de una expresión EL. Si se necesita usar el literal `${` en la salida, se debe escapar el carácter con una barra invertida: `\${`.

### Palabras Reservadas

Las siguientes palabras son **reservadas** en EL y no se deben utilizar como identificadores:

- `and`, `or`, `not`, `eq`, `ne`, `lt`, `gt`, `le`, `ge`, `true`, `false`, `null`, `instanceof`, `div`, `mod`, `empty`

### Operadores `[]` y `.`

En EL, se puede acceder a las propiedades de un objeto utilizando los operadores `[]` o `.`. Ambos tienen una función similar, aunque `[]` permite el acceso a propiedades cuyos nombres no son válidos como identificadores Java, como por ejemplo, aquellos que contienen caracteres especiales.

Ejemplos de acceso a propiedades:

```jsp
${objeto["propiedad"]}
${objeto.propiedad}
```

Si se necesita acceder a una propiedad cuyo nombre no es un identificador Java válido (por ejemplo, `accept-language`), se debe usar el operador `[]`:

```jsp
${request["accept-language"]}
```

Para acceder a propiedades anidadas, se usan los operadores de forma recursiva:

```jsp
${objeto.interior.propiedad}
${objeto["interior"]["propiedad"]}
```

### Evaluación de Expresiones EL

La evaluación de una expresión EL se realiza de **izquierda a derecha**. Para una expresión de la forma `expr-a[expr-b]`, el proceso de evaluación es el siguiente:

1. Se evalúa `expr-a` para obtener `valor-a`.
2. Si `valor-a` es `null`, se devuelve `null`.
3. Se evalúa `expr-b` para obtener `valor-b`.
4. Si `valor-b` es `null`, se devuelve `null`.
5. Dependiendo del tipo de `valor-a`:
   - Si es un **Map**, se devuelve el valor asociado a `valor-b`.
   - Si es una **List** o un **array**, se convierte `valor-b` a un `int` y se devuelve el valor correspondiente (si el índice está fuera de límites, se devuelve `null`).
   - Si no es ninguna de estas estructuras, `valor-a` debe ser un **JavaBean** y se intenta acceder a la propiedad `valor-b` a través del getter correspondiente.

## Acceso a JavaBeans

Tanto el operador `.` como `[]` se pueden usar para acceder a las propiedades de un **JavaBean**:

```jsp
${bean.nombrePropiedad}
${bean["nombrePropiedad"]}
```

Si una propiedad también tiene una propiedad interna, se puede acceder de manera recursiva.

## Objetos Implícitos en EL

EL proporciona varios **objetos implícitos** que pueden ser accedidos directamente dentro de las expresiones. Estos objetos proporcionan acceso directo a diferentes ámbitos y datos de la aplicación. Algunos de los objetos implícitos más comunes son:

| Objeto             | Descripción |
|--------------------|-------------|
| **pageContext**    | Proporciona acceso al contexto de la página JSP actual (`javax.servlet.jsp.PageContext`). |
| **initParam**      | Accede a los parámetros de inicialización del contexto de la aplicación como un **Map**. |
| **param**          | Representa los parámetros de la petición. Devuelve el primer valor si hay múltiples. |
| **paramValues**    | Similar a `param`, pero devuelve un **array** con todos los valores para un parámetro. |
| **header**         | Proporciona acceso a las cabeceras HTTP de la petición. |
| **headerValues**   | Similar a `header`, pero devuelve todos los valores posibles de una cabecera como un array. |
| **cookies**        | Permite acceder a las cookies disponibles en la petición. |
| **applicationScope** | Acceso a los atributos en el ámbito del contexto de la aplicación. |
| **sessionScope**   | Acceso a los atributos de la sesión del usuario. |
| **requestScope**   | Acceso a los atributos en el ámbito de la petición. |
| **pageScope**      | Acceso a los atributos en el ámbito de la página JSP. |

### Ejemplos de Uso de Objetos Implícitos

- Para obtener un parámetro de petición llamado `userName`:

  ```jsp
  ${param.userName}
  ${param["userName"]}
  ```

- Para acceder a una cabecera HTTP como `accept-language`:

  ```jsp
  ${header["accept-language"]}
  ```

- Para acceder al valor de una cookie llamada `sessionId`:

  ```jsp
  ${cookies.sessionId.value}
  ```

## Otros Operadores en EL

EL proporciona una serie de **operadores** que permiten realizar operaciones aritméticas, lógicas, relacionales y condicionales.

### Operadores Aritméticos

- Adición: `+`
- Sustracción: `-`
- Multiplicación: `*`
- División: `/` o `div`
- Módulo: `%` o `mod`

### Operadores Relacionales

- Igualdad: `==` o `eq`
- Desigualdad: `!=` o `ne`
- Mayor que: `>` o `gt`
- Mayor o igual que: `>=` o `ge`
- Menor que: `<` o `lt`
- Menor o igual que: `<=` o `le`

### Operadores Lógicos

- **AND**: `&&` o `and`
- **OR**: `||` o `or`
- **NOT**: `!` o `not`

### Operador Condicional

El operador condicional tiene la siguiente sintaxis:

```jsp
${expresion ? valor_si_verdadero : valor_si_falso}
```

Si la `expresion` se evalúa como verdadera, devuelve `valor_si_verdadero`, en caso contrario devuelve `valor_si_falso`.

### Operador `empty`

El operador **`empty`** se usa para verificar si un valor es `null` o está vacío. Devuelve `true` si el valor es `null`, una cadena de longitud cero, una colección o un array vacío.

```jsp
${empty listaDeUsuarios}
```

## Configuración de EL en las Versiones Modernas de JSP

Con las versiones **JSP 2.0** y posteriores, se permite inhabilitar tanto el scripting como el uso del Lenguaje de Expresión (EL), dependiendo de las necesidades del proyecto. Esta característica ayuda a fomentar la creación de **páginas más limpias y mejor estructuradas**.

### Inhabilitar Scripting en JSP

Para inhabilitar los **elementos de scripting** en una página JSP, se puede utilizar el siguiente fragmento en el descriptor de despliegue (`web.xml`):

```xml
<jsp-config>
    <jsp-property-group>
        <url-pattern>*.jsp</url-pattern>
        <scripting-invalid>true</scripting-invalid>
    </jsp-property-group>
</jsp-config>
```

### Desactivar la Evaluación de EL

Para desactivar la evaluación de EL en una página JSP específica, se puede hacer de dos formas:

1. Utilizando el atributo `isELIgnored` en la directiva `@page`:

    ```jsp
    <%@ page isELIgnored="true" %>
    ```

2. Configurando el descriptor de despliegue (`web.xml`) para desactivar EL en todas las páginas que coincidan con un patrón específico:

    ```xml
    <jsp-config>
        <jsp-property-group>
            <url-pattern>*.jsp</url-pattern>
            <el-ignore>true</el-ignore>
        </jsp-property-group>
    </jsp-config>
    ```

Estas configuraciones son útiles para garantizar que la lógica de negocio no se mezcle con la lógica de presentación, promoviendo la **separación de responsabilidades** y el mantenimiento de un **código más limpio y mantenible**.

## Comparativa con el Paradigma Actual

En el contexto del **desarrollo moderno de servidores**, **EL** se ha convertido en una herramienta esencial para minimizar el uso de código Java directamente en las páginas JSP. Con el avance de frameworks como **Spring** y la integración con **JSTL** (JSP Standard Tag Library), la mayor parte de la lógica que antes se incluía en scriptlets ahora se maneja mediante **controladores** y **servicios**. Esta arquitectura permite una **mayor modularidad** y una separación clara entre la vista y la lógica de negocio, alineándose con principios como **MVC (Model-View-Controller)** y **Separation of Concerns**.

El uso de EL junto con **JSTL** y la creciente preferencia por frameworks **JavaServer Faces (JSF)**, **Thymeleaf** o **Spring MVC** ha hecho que la lógica de las páginas sea más declarativa y orientada a atributos, mejorando la **mantenibilidad** y la **escalabilidad** de las aplicaciones web. De este modo, la **expresión EL** se considera una pieza importante en la evolución hacia aplicaciones web **más limpias, reutilizables y fáciles de entender**.
