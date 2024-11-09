# Guía para Instalar un Servidor con Nginx en una Máquina Virtual Debian


---

## **1. Configuración Básica y Permisos de Sudo**

### Crear un nuevo usuario con permisos sudo

1. Inicia sesión en tu máquina virtual como **root**. (COMO ROOT! NO COMO TU USUARIO)

3. Agrega el usuario al grupo `sudo`:

   ```bash
   usermod -aG sudo tu_usuario
   ```

4. Inicia sesión con el nuevo usuario:

   ```bash
   su - tu_usuario
   ```

---

## **2. Configurar SSH para Conexión desde el Host**


### Conectar desde el host a la máquina virtual

1. Desde tu máquina host, abre una terminal.

2. Conéctate a la VM usando SSH:

   ```bash
   ssh tu_usuario@ip_de_la_vm
   ```

---

## **3. Autenticación con Clave Pública y Privada**

### Generar y copiar claves SSH

1. En el host, genera un par de claves SSH (si no lo has hecho):

   ```bash
   ssh-keygen -t rsa -b 4096
   ```

2. Copia la clave pública al servidor manualmente:

   - Abre el archivo `id_rsa.pub` en tu host y copia su contenido.
   - En la máquina virtual, conéctate y crea el directorio `.ssh` (si no existe):

     ```bash
     mkdir -p ~/.ssh
     ```
   - Pega la clave en el archivo `~/.ssh/authorized_keys`:

     ```bash
     echo "tu_clave_publica" >> ~/.ssh/authorized_keys
     ```

3. Ajusta los permisos:

   ```bash
   chmod 600 ~/.ssh/authorized_keys
   chmod 700 ~/.ssh
   ```

---

## **4. Instalar y Configurar el Servidor Nginx**

### Instalar Nginx

1. Actualiza los paquetes:

   ```bash
   sudo apt update
   ```

2. Instala Nginx:

   ```bash
   sudo apt install nginx
   ```

3. Verifica que Nginx esté corriendo:

   ```bash
   sudo systemctl status nginx
   ```

### Permitir tráfico HTTP y HTTPS en el firewall (si está habilitado)

```bash
sudo ufw allow 'Nginx Full'
```

---

## **5. Crear una Carpeta con el Sitio Web y Habilitarlo**

### Crear Directorio para el Sitio Web

1. Crea el directorio:

   ```bash
   sudo mkdir -p /var/www/tu_dominio.com/html
   ```

2. Asigna los permisos:

   ```bash
   sudo chown -R $USER:$USER /var/www/tu_dominio.com/html
   sudo chmod -R 755 /var/www
   ```

### Crear una Página Web de Ejemplo

```bash
nano /var/www/tu_dominio.com/html/index.html
```

*Agrega contenido HTML básico y guarda el archivo.*

### Configurar Nginx para el Sitio

1. Crea un archivo de configuración:

   ```bash
   sudo nano /etc/nginx/sites-available/tu_dominio.com
   ```

2. Agrega la siguiente configuración:

   ```
   server {
       listen 80;
       server_name tu_dominio.com www.tu_dominio.com;

       root /var/www/tu_dominio.com/html;
       index index.html index.htm;

       location / {
           try_files $uri $uri/ =404;
       }
   }
   ```

3. Habilita el sitio:

   ```bash
   sudo ln -s /etc/nginx/sites-available/tu_dominio.com /etc/nginx/sites-enabled/
   ```

4. Verifica la configuración y reinicia Nginx:

   ```bash
   sudo nginx -t
   sudo systemctl restart nginx
   ```

---

## **6. Configurar Múltiples Dominios**

### Repetir el Proceso para Cada Dominio

1. Crea directorios separados para cada dominio:

   ```bash
   sudo mkdir -p /var/www/otro_dominio.com/html
   ```

2. Configura los permisos y crea páginas de ejemplo.

3. Crea archivos de configuración en `/etc/nginx/sites-available/` para cada dominio.

4. Habilita cada sitio con un enlace simbólico en `/etc/nginx/sites-enabled/`.

5. Verifica y reinicia Nginx después de cada configuración.

---

## **7. Configurar FTP y SFTP**

### Instalar y Configurar vsftpd (Opcional)

**Nota:** Por razones de seguridad, se recomienda usar SFTP en lugar de FTP. Sin embargo, si necesitas FTP:

**Instalar vsftpd:**

```bash
sudo apt install vsftpd
```

**Configurar vsftpd:**

1. Edita el archivo de configuración:

   ```bash
   sudo nano /etc/vsftpd.conf
   ```

2. Modifica las siguientes líneas:

   ```
   anonymous_enable=NO
   local_enable=YES
   write_enable=YES
   chroot_local_user=YES
   ```

3. Reinicia el servicio:

   ```bash
   sudo systemctl restart vsftpd
   ```

### Configurar SFTP con OpenSSH

1. Crea un grupo para usuarios SFTP:

   ```bash
   sudo groupadd sftpusers
   ```

2. Agrega usuarios al grupo:

   ```bash
   sudo usermod -aG sftpusers tu_usuario_sftp
   ```

3. Edita el archivo de configuración SSH:

   ```bash
   sudo nano /etc/ssh/sshd_config
   ```

4. Agrega al final del archivo:

   ```
   Match Group sftpusers
       ChrootDirectory /home/%u
       ForceCommand internal-sftp
       X11Forwarding no
       AllowTcpForwarding no
   ```

5. Asegúrate de que el directorio de chroot sea propiedad de root:

   ```bash
   sudo chown root:root /home/tu_usuario_sftp
   sudo chmod 755 /home/tu_usuario_sftp
   ```

6. Crea un directorio para archivos dentro del chroot:

   ```bash
   sudo mkdir /home/tu_usuario_sftp/files
   sudo chown tu_usuario_sftp:sftpusers /home/tu_usuario_sftp/files
   ```

7. Reinicia el servicio SSH:

   ```bash
   sudo systemctl restart ssh
   ```

---

## **8. Configurar HTTPS con Let's Encrypt**

### Instalar Certbot y Obtener Certificados SSL

1. Instala Certbot y el plugin de Nginx:

   ```bash
   sudo apt install certbot python3-certbot-nginx
   ```

2. Obtén y configura el certificado SSL:

   ```bash
   sudo certbot --nginx -d tu_dominio.com -d www.tu_dominio.com
   ```

3. Sigue las instrucciones interactivas para completar la instalación.

### Configurar Redirección de HTTP a HTTPS

Certbot puede configurar automáticamente la redirección. Si necesitas hacerlo manualmente:

1. Edita el archivo de configuración de Nginx:

   ```bash
   sudo nano /etc/nginx/sites-available/tu_dominio.com
   ```

2. Agrega una redirección en el bloque del servidor que escucha en el puerto 80:

   ```
   server {
       listen 80;
       server_name tu_dominio.com www.tu_dominio.com;
       return 301 https://$host$request_uri;
   }
   ```

---

**¡Felicidades!** Ahora tienes un servidor Debian configurado con Nginx, múltiples sitios web, acceso SSH seguro, FTP/SFTP y soporte para HTTPS con certificados SSL.

---

### Nota adicional
- **Seguridad:** Siempre es importante mantener tu sistema actualizado y aplicar buenas prácticas de seguridad.
- **Renovación de certificados:** Si usas Let's Encrypt, los certificados expiran cada 90 días. Certbot configura automáticamente la renovación, pero puedes verificarlo:
  
  ```bash
  sudo certbot renew --dry-run
  ```

- **Documentación:** Consulta la documentación oficial de Debian y Nginx para profundizar en configuraciones avanzadas.