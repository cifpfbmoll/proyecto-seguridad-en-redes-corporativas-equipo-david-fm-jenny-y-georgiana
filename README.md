[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/A04QAW6X)
------------------Script 1------------------------
...
------------------Script 2------------------------
...
------------------Script 3-------------------------
**los Comandos:**

*1--instalación*
sudo apt update
sudo apt install apache2

*2--Configuraciones globales*
sudo nano /etc/apache2/apache2.conf

*3--ocultacion de versiones*
sudo nano /etc/apache2/conf-available/security.conf

*4--exposicion minima de módulos*
sudo a2dismod status

*5--Creación virtualhost*
sudo nano /etc/apache2/sites-available/mi_nombre_mi_apellido.conf
--Configuracion múltimple de contexto:directiva options
<Directory /var/www/html>
    Options -Indexes +FollowSymLinks
</Directory>

*6--ficheros .htaccess*
permiten configurar ajustes por directorio en Apache
sudo nano /var/www/html/.htaccess

*7--HTTPS*
sudo apt install openssl
openssl req -new -newkey rsa:2048 -nodes -keyout /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.csr
openssl x509 -req -days 365 -in /etc/ssl/certs/apache-selfsigned.csr -signkey /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt
sudo nano /etc/apache2/sites-available/default-ssl.conf

*8--Módulo mod-Security*
Es un módulo que proporciona protección contra amenazas como ataques SQL injection, cross-site scripting, etc.
sudo apt install libapache2-mod-security2
sudo a2enmod security2
sudo systemctl restart apache2

*9--ataques kali linux*
git clone https://github.com/SpiderLabs/owasp-modsecurity-crs.git /etc/modsecurity/
cp /etc/modsecurity/crs-setup.conf.example /etc/modsecurity/crs-setup.conf

*10--habilitar mod_security*
sudo nano /etc/modsecurity/modsecurity.conf
"SecRuleEngine On"

*11-verificar protección* 
sudo tail -f /var/log/apache2/error.log

----------------------------------Script 4------------------------------------

0-Actualizar todos los paquetes:
sudo apt update

1-Instalar SSH:
sudo apt install openssh-server

2-Verificar que el servicio funciona correctamente:
sudo systemctl status ssh

ACTIVIDADES-->
1-Autenticación SSH basada en clave pública:

2-Añadir PubkeyAuthentication yes al archivo de configuración.

3-Cambio de puerto por defecto:

Añadir "Port 300" al archivo de configuración "sshd_config".

4-Vinculación IP:

poner como por ejemplo ListenAddress 192.168.1.117

5-Deshabilitar el usuario ROOT para login:

Añadir "PermitRootLogin no" al archivo de configuración.

6-Limitar el acceso SSH de los usuarios del sistema:

Añadir AllowUsers user1 user2 al archivo de configuración.
un ejemplo mas vizual: AllowUsers gcretu cretu georgi.

7-Deshabilitar inicio de sesión basado en contraseña:

Añadir "PasswordAuthentication no" al archivo de configuración.

8-Deshabilitar contraseñas vacías:

Añadir "PermitEmptyPasswords no" al archivo de configuración.

9-Limitar intentos de autenticación fallida:

Añadir "MaxAuthTries 3" al archivo de configuración.

10-Limitar conexiones simultáneas no autenticadas:

Añadir "MaxStartups 3" al archivo de configuración.

11-Habilitar un banner de advertencia para los usuarios de SSH:

Añadir "Banner /etc/issue" al archivo de configuración.

12-Configurar el intervalo de tiempo de espera de cierre de sesión inactiva:

Añadir "ClientAliveCountMax 0" y "ClientAliveInterval 300" al archivo de configuración.

13-Deshabilitar X11 forwarding:

Añadir "X11Forwarding no" al archivo de configuración.

14-Bloquear usuarios a sus directorios de inicio (Chroot):

Crear el directorio jaula y configurar los permisos necesarios.

15-Habilitar doble factor de autenticación en SSH:

Instalar Google Authenticator:
"sudo apt install libpam-google-authenticator"
Configurar PAM: (añadir lo siguiente en la configuración pam)
"auth required pam_google_authenticator.so"
Reiniciar el servicio SSH:
"sudo systemctl restart sshd.service"

-Modificar lo siguiente de "sshd_config"
ChallengeResponseAuthentication yes
UsePAM yes
PasswordAuthentication no

-Poner en la termnal "google-authenticator"
-Descargar la aplicacion de autentificar de google para así escanear el QR 
-Responder a las preguntas de configuración de Google Authenticator:
Make tokens time-based: yes
Update the .google_authenticator file: yes
Disallow multiple uses: yes
Increase the original generation time limit: no
Enable rate-limiting: yes

(y sa tendria que funcionar.)

