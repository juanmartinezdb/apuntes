# COMANDOS DE LINUX

### Introducción al Prompt de Comandos

En Linux, el prompt muestra información esencial sobre el usuario y la ubicación actual en el sistema de archivos:

`pepe@patation:~$`

- **pepe**: Nombre del usuario.
- **patation**: Nombre de la máquina.
- **~**: Directorio home del usuario actual.
- **$**: Indica que el usuario no tiene privilegios de root.
- **#**: Indica que el comando se ejecuta como root.

## Sistema de Archivos

- `/` - Directorio raíz, la base del sistema de archivos.
- `/dev` - Directorio para dispositivos de hardware.
    - `/sr0` - Representa unidades de CD-ROM.
    - `/sda1` - Representa la primera partición del primer disco duro.
- `/home` - Directorio similar a "Users" en Windows, contiene los directorios personales de los usuarios.
- `/boot` - Contiene archivos necesarios para el arranque del sistema.
    - `/efi` - Directorio para sistemas con EFI (Extensible Firmware Interface).
- `/etc`: Archivos de configuración del sistema
- `/var`: Información variable del sistema
    - `/var/log`: Archivos de registro (logs)
- `/etc/sudoers`: Archivo de configuración de usuarios con privilegios de superusuario (sudo)
- `/etc/sudoers.d`: Directorio para ampliar la configuración de `sudoers`
## Comandos básicos

- `sudo adduser nombre`: Añadir un nuevo usuario
- `pwd`: Imprimir el directorio de trabajo actual
- `ls`: Ver el contenido de un directorio
    - `-l`: Formato extendido
    - `-a`: Mostrar archivos ocultos
    - `-R`: Recursivo
    - `-r`: Inverso
- `cp`: Copiar archivos y carpetas
    - `-v`: Explicar la operación de copiado
    - `-p`: Preservar los atributos
    - `-b`: Hacer una copia de seguridad de los archivos
- `mkdir`: Crear un nuevo directorio
    - `-p`: Crear directorios intermedios si es necesario
- `rm`: Eliminar archivos y directorios
    - `-i`: Preguntar antes de eliminar
    - `-v`: Explicar la operación de eliminación
- `cat`: Imprimir el contenido de un archivo en la consola
    - `-n`: Numerar todas las líneas
    - `-b`: Numerar las líneas que no están en blanco
    - `-s`: Agrupar líneas en blanco consecutivas
- `wc`: Contar palabras, líneas y caracteres
    - `-l`: Sólo líneas
    - `-w`: Sólo palabras
    - `-c`: Sólo caracteres
- `history`: Mostrar el historial de comandos
- `date`: Mostrar y cambiar la fecha y hora del sistema
- `adduser`: Manipular grupos de usuarios
- `more`: Mostrar el contenido de un archivo por pantallas
- `less`: Similar a `more`, pero permite desplazarse hacia arriba y abajo
## Gestión de Archivos y Directorios

### Tipos de Archivos

- **b**: Archivo de dispositivo de bloque (por ejemplo, discos duros).
- **c**: Archivo de dispositivo de caracteres (por ejemplo, terminales o impresoras). donde la maquina lee un byt o escribe un byte.
- **d**: Directorio.
- **l**: Enlace simbólico.
- **-**: Archivo regular.

# Usuarios y grupos
### Permisos de archivos

- `r` (read): Permiso de lectura (4)
- `w` (write): Permiso de escritura (2)
- `x` (execute): Permiso de ejecución (1)
- Ejemplo: `rwx` (7) = lectura, escritura y ejecución

Los permisos se dividen en tres grupos de tres dígitos:

1. Propietario del archivo `u`
2. Grupo al que pertenece el archivo `g`
3. Otros usuarios `o`

    - `chown usuario:grupo archivo`: Cambia el propietario y el grupo de un archivo.
    - `chmod +x archivo`: Hace un archivo ejecutable para todos los usuarios.
    - `chmod o=rx` (solo escritura y ejecucion)
    - `chmod 0+rx` (se SUMA esos permisos a los anteriores)
    
- `/etc/group`: Archivo que contiene los grupos de usuarios
- `/etc/passwd`: Archivo que contiene los usuarios del sistema
- `id`: Comando para ver la información de usuario y grupo actual
- `chown usuario archivo`: Cambiar el propietario de un archivo
- `chgrp grupo archivo`: Cambiar el grupo de un archivo
    - `-R`: Recursivo
    - `-v`: Modo detallado
    - 
## Herramientas y Comandos

### Gestión de Paquetes y Software

- **sudo apt update**: Actualiza la lista de paquetes disponibles.
- **sudo apt upgrade**: Actualiza los paquetes a las últimas versiones disponibles.
- **dpkg**: Gestiona paquetes a nivel bajo, requiere que el archivo del paquete esté localmente.
- **apt**: Gestiona paquetes desde repositorios en línea, interfaz de alto nivel más amigable.

### Herramientas de Red

- **ip a**: Muestra información de las interfaces de red y sus configuraciones IP.
- **tty**: Representa una terminal física.
- **pts**: Terminales virtuales, como las utilizadas en conexiones SSH.

### Scripts

- **Bash scripts**: Comienzan con `#!/bin/bash` para indicar el intérprete de comandos.
- **Control de Procesos**:
    - **htop**: Visualizador interactivo de procesos que permite gestionarlos fácilmente.
    - **kill**: Envía señales a los procesos para su terminación.
        - `kill -9 [PID]`: Termina un proceso de forma inmediata.

### Redirección y Gestión de Logs

- **Redirección de errores**: `comando 2> /dev/null` envía los errores a un lugar donde serán ignorados.
- **Tail y Head**:
    - `tail -n 10 archivo`: Muestra las últimas 10 líneas de un archivo.
    - `head -n 10 archivo`: Muestra las primeras 10 líneas de un archivo.

## Trucos y Consejos

- **!!**: Ejecuta el último comando ingresado en la terminal.
- **echo $PATH**: Muestra las rutas en la variable de entorno PATH, donde el sistema busca los ejecutables.


## Preparación para Exámenes

Conocimientos fundamentales para exámenes sobre Linux generalmente incluyen:

- Instalación y configuración de software.
- Localización y gestión de archivos de configuración.
- Monitorización de logs y procesos en ejecución.
- Uso eficaz de comandos para resolver problemas específicos propuestos.
  
  ### Herramientas de Descarga

- **curl**: Una herramienta moderna para descargar archivos desde la línea de comandos. Soporta múltiples protocolos.
- **wget**: Una herramienta más antigua comparada con curl, utilizada para descargar archivos desde la línea de comandos.

### Gestión de Paquetes con dpkg y apt

- **.deb**: Archivos de paquete para sistemas basados en Debian, como Ubuntu. Contienen todos los archivos necesarios para instalar una aplicación, así como scripts para configurarla.
- **dpkg**: Herramienta de bajo nivel que puede instalar, desinstalar, y listar paquetes Debian, pero requiere que el paquete esté descargado localmente.
- **apt**: Herramienta de alto nivel más amigable, que maneja la descarga e instalación de paquetes desde repositorios remotos, simplificando la gestión de software.

### Extensión de Archivos Comprimidos en Linux

- **gz**: Formato de compresión gzip.
- **tar**: Archivo que puede contener múltiples archivos o directorios.
- **tar.gz**: Archivo tar comprimido con gzip.
- **bz, bz2**: Archivos comprimidos usando bzip2.
- **deb**: Formato de paquete más común en sistemas Debian y derivados.

### Comandos de Red y Sistema

- `systemctl status`: Comando para verificar el estado de servicios en el sistema.
- `apt search -n [nombre]:` Busca paquetes por nombre en los repositorios configurados.
- `ip a:` Muestra información sobre las interfaces de red y sus direcciones IP.

### Terminales y Consolas

- **tty**: Representa una terminal directa del sistema, usualmente física.
- **pts**: Pseudo-terminal slave, terminales virtuales creadas, por ejemplo, al conectarse a través de SSH.

### Gestión de Permisos y Propietarios

- **`chmod +x [archivo]`**: Concede permisos de ejecución a todos los usuarios para un archivo específico.
- **`chmod o=rx [archivo]`**: Establece permisos de lectura y ejecución solo para otros (usuarios que no son ni el propietario ni del grupo).
- **`chown [usuario]:[grupo] [archivo]`**: Cambia tanto el propietario como el grupo de un archivo.
- **`chgrp`**: Cambia el grupo de un archivo de manera recursiva y verbosa con `-R -v`.

### Procesos y Prioridades

- **Nice**: Valor que determina la prioridad de los procesos en Linux. Un valor más bajo significa mayor prioridad.
- **PID (Process ID)**: Identificador único para cada proceso en ejecución.
- **`htop`**: Herramienta para visualizar y gestionar procesos activos, donde se puede enviar señales a procesos, como SIGTERM para terminación amable o SIGKILL para forzar la terminación.
- **`kill -9 [PID]`**: Comando que envía la señal SIGKILL a un proceso para terminarlo inmediatamente.
- **`ps`**: Muestra información sobre los procesos en ejecución.

### Scripts y Automatización

- **Scripts de Bash**: Archivos de script que comienzan con `#!/bin/bash` para indicar que se ejecutarán usando el intérprete de Bash.
- **`watch [comando]`**: Ejecuta un comando específico periódicamente (cada dos segundos por defecto) y muestra la salida.