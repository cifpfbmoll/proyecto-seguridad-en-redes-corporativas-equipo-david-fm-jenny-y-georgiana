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

--------------------------------Sprint 5-------------------------------->
1. Descargar Metasploitable2
Conseguir la IPs de las maquinas en las que se quiere hacer los escaners

-->Para hacer los escaners siguiente más practico (si hya que hacer esner a la dos maquinas virtuales ) hacerlo junto en un mismo comando poniendo las dos ips. (por ejemplo "ip1"-->Metasploitable2 y "ip2"--> Ubuntu server). 

2. Escaneo SYN Scan
   
Comando:nmap -sS (ip1) (ip2)

Descripción: Realiza un escaneo SYN, también conocido como "half-open" scan, que es más rápido y menos detectable, permitiendo identificar los principales servicios y puertos abiertos en las IPs especificadas.

3. Escaneo de Puertos UDP
Comando:nmap -sU (ip1) (ip2)

Descripción: Realiza un escaneo de los principales puertos UDP abiertos en Metasploitable2 y Ubuntu Server, identificando servicios esenciales que utilizan el protocolo UDP.

4. Escaneo con Script de Vulnerabilidades
Comando:
nmap --script vuln (ip1) (ip2)

Descripción: Ejecuta el script vuln de Nmap, que detecta varias vulnerabilidades conocidas en los sistemas objetivo, proporcionando información sobre posibles puntos débiles.

6. Escaneo Agresivo
Comando:nmap -A (ip1) (ip2)

Descripción: Realiza un escaneo agresivo que incluye detección del sistema operativo, versión del servicio, escaneo de scripts y traceroute, proporcionando una visión de los objetivos.

6. Escaneo de Descubrimiento de Equipos en la Red Doméstica
Comando: nmap -sn 192.168.1.0/24 (red local)

Descripción: Realiza un escaneo de descubrimiento de equipos en la red local, identificando todos los dispositivos conectados sin realizar un escaneo de puertos completo.
----------------------------------Script 6------------------------------------
_______________________________________
Como poner la reglas en cada caso-->
_______________________________________
1. Tener Internet desde el servidor
Accede a la interfaz de pfSense.
Ve a Firewall, Rules en DMZ, añadir-->
Action: Pass
Interface: DMZ
Address Family: IPv4
Protocol: Any
Source: Network 10.0.3.0/24 (DMZ)
Destination: Any

(Guarda y aplica los cambios)

2. Internet desde el equipo de los empleados
Ve a Firewall, Rules en Pestaña LAN y añadir-->
Action: Pass
Interface: LAN 
Address Family: IPv4
Protocol: Any
Source: LAN addresses
Destination: Any

(Guarda y aplica los cambios)

4. Servidor web únicamente por el puerto 443 y redirigir tráfico del puerto 80 al 44 , (en reglas, la pestaña DMZ,añdir)

Action: Pass
Interface: DMZ
Address Family: IPv4
Protocol: TCP
Source: Any
Destination: Network 10.0.3.0/24 (DMZ)
Destination Port Range: 443

-->En Firewall en NAT-->Pestaña Port Forward, añadir

Interface: WAN
Protocol: TCP
Destination Address: WAN Address
Destination Port Range: 80
Redirect Target IP: IP del servidor en DMZ
Redirect Target Port: 443

(Guarda y aplica los cambios)

4. Hacer accesible el servidor SSH únicamente desde el puerto elegido en el sprint de Hardening SSH .
En Firewall en Rules, pestaña DMZ.

Haz clic en el botón Add para crear una nueva regla.

Action: Pass
Interface: DMZ
Address Family: IPv4
Protocol: TCP
Source: Any
Destination: DMZ subnets
Destination Port Range: puerto 22 SSH

(Guarda y aplica los cambios)

5. Bloquear tráfico directo entre el servidor y los empleados (en ambos sentidos)
Firewall -->Rules, pestaña DMZ, añadir

Action: Block
Interface: DMZ
Address Family: IPv4
Protocol: Any
Source: Network 10.0.3.0/24 (DMZ)
Destination:LAN subnets

(Guarda la configuración)
(Repite los pasos anteriores en la pestaña LAN (Empleados), invirtiendo las redes de origen y destino)

6. regla que bloquee el tráfico en caso de ciberataque
Firewall -> Rules, pestaña DMZ, en añadir

Action: Block
Interface: DMZ
Address Family: IPv4
Protocol: Any
Source: DMZ subnets
Destination: Any

(Guarda)

(Para deshabilitar la regla)

7. Bloquear tráfico de IP específica en caso de ataque DoS
Ve a Firewall > Rules, pestaña DMZ.

Action: Block
Interface: DMZ
Address Family: IPv4
Protocol: Any
Source: IP atacante
Destination: DMZ subnets
(Guarda)

