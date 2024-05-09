# Procedimiento para Modificar Contraseñas en Windows desde un Entorno de Arranque Seguro

Este procedimiento detalla los pasos necesarios para modificar contraseñas en sistemas Windows desde un entorno de arranque seguro utilizando herramientas de pentesting.

## 1. Preparación del Entorno de Penetración:
- Utiliza una distribución de pentesting como Kali Linux o Parrot OS desde un dispositivo USB.
- Arranca el sistema desde el USB para acceder a un entorno de arranque seguro y no intrusivo.

## 2. Identificación y Navegación en el Disco de Windows:
- Identifica la ubicación del disco donde está instalado Windows, generalmente bajo letras de unidad como C:\, D:\, etc.
- Accede a la carpeta System32 en el disco de Windows para manipular archivos relacionados con la seguridad del sistema.

## 3. Utilización de Herramientas de Manipulación de Contraseñas:
- Abre una terminal en el entorno de pentesting.
- Utiliza la herramienta `chntpw` con privilegios elevados (`sudo`) para listar los usuarios del sistema Windows y sus respectivas contraseñas hash.

## 4. Eliminación de Contraseña (Opción 1):
- Ejecuta el comando `sudo chntpw -u usuario SAM`, donde "usuario" es el nombre del usuario cuya contraseña deseas eliminar.
- Al seleccionar esta opción, se modificará la base de datos SAM para eliminar la contraseña del usuario especificado.

## 5. Creación de un Nuevo Usuario Administrador (Opción 2):
- Si prefieres una solución más segura, crea un nuevo usuario administrador en la base de datos SAM.
- Asigna este nuevo usuario al grupo 220 para otorgarle privilegios administrativos completos.

## 6. Reinicio y Confirmación de Cambios:
- Reinicia el sistema Windows utilizando el comando `reboot -h now` desde la terminal del entorno de pentesting.
- Después del reinicio, prueba iniciar sesión con el usuario modificado o el nuevo usuario administrador creado.

Es crucial tener un conocimiento profundo de las implicaciones de seguridad al realizar este tipo de modificaciones en un sistema operativo. Este procedimiento debe llevarse a cabo con cuidado y en un entorno controlado para evitar consecuencias no deseadas en la integridad del sistema.

---

Este README proporciona una guía clara y concisa para llevar a cabo operaciones de modificación de contraseñas en sistemas Windows desde un entorno seguro. Si tienes alguna pregunta o necesitas más detalles sobre algún paso, no dudes en consultar.
