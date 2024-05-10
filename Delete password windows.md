## Procedimiento para Modificar Contraseñas en Windows desde un Entorno de Arranque Seguro y Pentesting

Este procedimiento detalla los pasos necesarios para modificar contraseñas en sistemas Windows desde un entorno de pentesting utilizando herramientas como Kali Linux o Parrot OS.

### 1. Preparación del Entorno:
- Inicia tu dispositivo USB con una distribución de pentesting como Kali Linux o Parrot OS.
- Asegúrate de que el disco no esté en modo "read-only" para poder realizar cambios.

### 2. Arranque con USB Booteable:
- Inserta el USB booteable y arranca desde él para acceder al entorno de arranque en vivo.

### 3. Navegación en el Disco Duro y Identificación:
- Identifica el disco donde está instalado Windows.
- Accede a la ruta `C:\Windows\System32\config` en el disco de Windows.

### 4. Manipulación de Contraseñas con chntpw:
- Abre una terminal y ejecuta `sudo chntpw -l SAM` para listar todos los usuarios del sistema.
- Utiliza `sudo chntpw -u usuario SAM` para seleccionar el usuario cuya contraseña deseas modificar.

#### Opción 1: Eliminar la Contraseña
- Elige la opción 1 para quitar la contraseña del usuario seleccionado.
- Confirma con Enter y luego escribe 'q', 'y' para guardar los cambios.
- Reinicia el sistema con `reboot -h now`. Ahora el usuario no tendrá contraseña.

#### Opción 2: Agregar un Nuevo Usuario Administrador
- Selecciona la opción 2 para agregar un nuevo usuario administrador.
- Asigna al nuevo usuario el grupo 220 para privilegios administrativos completos.
- Inicia sesión con este nuevo usuario y luego quita la contraseña del usuario original si es necesario.

### 5. Reinicio y Confirmación de Cambios:
- Reinicia el sistema Windows utilizando el comando `reboot -h now` desde la terminal del entorno de pentesting.
- Después del reinicio, prueba iniciar sesión con el usuario modificado o el nuevo usuario administrador creado.

Es esencial comprender las implicaciones de seguridad al realizar estos cambios y asegurarse de tener los permisos necesarios para realizar estas operaciones en sistemas Windows.

Este README proporciona una guía clara y concisa para llevar a cabo operaciones de modificación de contraseñas en sistemas Windows desde un entorno seguro. Si tienes alguna pregunta o necesitas más detalles sobre algún paso, no dudes en consultar.
