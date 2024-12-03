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






