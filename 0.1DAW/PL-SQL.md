### Tema 7. PL/SQL

---


##### 3.2. Primer programa

```sql
SET SERVEROUTPUT ON;

BEGIN
    DBMS_OUTPUT.PUT_LINE('Hola, Mundo!');
END;
/

```

##### 3.3. Lectura y Escritura

```sql
DBMS_OUTPUT.PUT_LINE('Texto a mostrar');
```

Para leer datos desde el teclado se usan variables de sustitución precedidas por `&`.

---

#### 4. Tipos de Datos

##### 4.1. Tipos de Datos Simples

- **Numéricos**: `NUMBER`, `INTEGER`, DEC, DECIMAL `PLS_INTEGER`
- **Alfanuméricos**: `CHAR`, `VARCHAR2`
- **Otros**: `BOOLEAN`, `DATE`

##### 4.2. Tipos de Datos Compuestos

###### 4.2.1. Cursores

**Cursor estático simple**:
```plsql
DECLARE
    CURSOR simple_cursor IS
        SELECT nombre FROM empleados;
BEGIN
    OPEN simple_cursor;
    FETCH simple_cursor INTO v_nombre;
    CLOSE simple_cursor;
END;
/

```


**Cursor estático parametrizado**:

sql

Copiar código

`DECLARE     CURSOR parametrizado_cursor (dept_id NUMBER) IS         SELECT nombre FROM empleados WHERE departamento_id = dept_id; BEGIN     OPEN parametrizado_cursor(10);     FETCH parametrizado_cursor INTO v_nombre;     CLOSE parametrizado_cursor; END; /`

**Cursor dinámico**:

sql

Copiar código

`DECLARE     TYPE ref_cursor IS REF CURSOR;     v_cursor ref_cursor;`
   

sql

Copiar código

    `v_nombre empleados.nombre%TYPE; BEGIN     OPEN v_cursor FOR 'SELECT nombre FROM empleados WHERE departamento_id = :dept_id' USING 10;     FETCH v_cursor INTO v_nombre;     CLOSE v_cursor; END; /`

###### 4.2.2. Registros

sql

Copiar código

`DECLARE     TYPE empleados_registro IS RECORD (         nombre empleados.nombre%TYPE,         salario empleados.salario%TYPE     );     v_empleado empleados_registro; BEGIN     v_empleado.nombre := 'Juan';     v_empleado.salario := 30000; END; /`

---

#### 5. El Bloque PL/SQL

sql

Copiar código

`DECLARE     v_nombre empleados.nombre%TYPE; BEGIN     SELECT nombre INTO v_nombre FROM empleados WHERE id = 1; EXCEPTION     WHEN NO_DATA_FOUND THEN         DBMS_OUTPUT.PUT_LINE('No se encontró el empleado.'); END; /`

---

#### 6. Zona de Declaración

###### 6.1. Declaración de Variables y Constantes

sql

Copiar código

`DECLARE     v_salario CONSTANT NUMBER := 30000;     v_nombre VARCHAR2(50); BEGIN     v_nombre := 'Pedro'; END; /`

###### 6.3. Declaración de Cursores

**Cursor estático simple**:

sql

Copiar código

`DECLARE     CURSOR simple_cursor IS         SELECT nombre FROM empleados; BEGIN     OPEN simple_cursor;     FETCH simple_cursor INTO v_nombre;     CLOSE simple_cursor; END; /`

**Cursor estático parametrizado**:

sql

Copiar código

`DECLARE     CURSOR parametrizado_cursor (dept_id NUMBER) IS         SELECT nombre FROM empleados WHERE departamento_id = dept_id; BEGIN     OPEN parametrizado_cursor(10);     FETCH parametrizado_cursor INTO v_nombre;     CLOSE parametrizado_cursor; END; /`

---

#### 7. Zona de Proceso

###### 7.1. Sentencias Propias de PL/SQL

**Condicional simple: IF-THEN**

sql

Copiar código

`IF v_salario > 25000 THEN     DBMS_OUTPUT.PUT_LINE('Salario alto'); END IF; /`

**Condicional múltiple: IF-THEN-ELSIF**

sql

Copiar código

`IF v_salario > 30000 THEN     DBMS_OUTPUT.PUT_LINE('Salario muy alto'); ELSIF v_salario > 25000 THEN     DBMS_OUTPUT.PUT_LINE('Salario alto'); ELSE     DBMS_OUTPUT.PUT_LINE('Salario bajo'); END IF; /`

**Bucle básico: LOOP**

sql

Copiar código

`LOOP     EXIT WHEN v_contador > 10;     v_contador := v_contador + 1; END LOOP; /`

**Bucle While**

sql

Copiar código

`WHILE v_contador <= 10 LOOP     DBMS_OUTPUT.PUT_LINE(v_contador);     v_contador := v_contador + 1; END LOOP; /`

**Bucle For**

sql

Copiar código

`FOR i IN 1..10 LOOP     DBMS_OUTPUT.PUT_LINE(i); END LOOP; /`

**Bucle sobre cursores**

sql

Copiar código

`FOR emp IN simple_cursor LOOP     DBMS_OUTPUT.PUT_LINE(emp.nombre); END LOOP; /`

---

#### 8. Excepciones

**Control de Errores**

sql

Copiar código

`BEGIN     SELECT nombre INTO v_nombre FROM empleados WHERE id = 1; EXCEPTION     WHEN NO_DATA_FOUND THEN         DBMS_OUTPUT.PUT_LINE('No se encontró el empleado.');     WHEN OTHERS THEN         DBMS_OUTPUT.PUT_LINE('Ocurrió un error.'); END; /`

**Definir y lanzar excepciones**

sql

Copiar código

`DECLARE     e_salario_bajo EXCEPTION; BEGIN     IF v_salario < 20000 THEN         RAISE e_salario_bajo;     END IF; EXCEPTION     WHEN e_salario_bajo THEN         DBMS_OUTPUT.PUT_LINE('El salario es demasiado bajo.'); END; /`