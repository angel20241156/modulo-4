Práctica 1 pt1
Sudo apt-get install apache2: Instalar apache 
Systemctl status apache2: para ver el estado 
Systemctl start apache2: para activarlo

Para crear el sito web : 
sudo nano /var/www/html/index.html
<html>
<h1>hola mundo<h1>
<html>
Control x para guardar 

Habilitar el sitio que vamos a crear:
Sudo Nano /etc/ache2/sites-available/pratica1.conf

<VirtualHost *:80>
       ServerAdmin webmaster@localhost
       DocumentRoot /var/www/html
       ErrorLog ${APACHE_LOG_DIR}/error.log
       CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
Control o para gurdar y x para salir 

Para activar el sitio:
Sudo a2ensite práctica1.conf

Ahora vamos a reiniciar el apache2:
Systemctl reload apache2 

Para probar 
http://Localhost
http://practica1.local

Práctica 1 pt2
Vamos a :
Sudo Nano /var/www/html/index.html
<html>
<h1>hola mundo<h1>
<html>
Control o y x 

Vamos a cambiar la configuración del sitio web 
Sudo Nano /etc/apache2/sites-available/practica1.conf

<VirtualHost *:8080>
       ServerAdmin webmaster@localhost
       DocumentRoot /var/www/html
       ErrorLog ${APACHE_LOG_DIR}/error.log
       CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
Control o para gurdar y x para salir 

Luego vamos a aquí que es donde se encuentra la configuración de los puertos 
Sudo Nano /etc/apache2/ports.conf
Control o para gurdar y x para salir 

Para activar el sitio:
Sudo a2ensite práctica1.conf

Ahora vamos a reiniciar el apache2:
Systemctl reload apache2 
Systemctl start apache2  

Para probar
127.0.0.1:8080

Práctica 2

Para actualizar y instalar los paquetes 
$ apt update -y && upgrade -y
Pasamos a instalar
$ apt install postfix -y

Vamos a configurarlo con este comando 
Sudo dpkg-reconfigure postfix

Luego creamos la siguiente carpeta con nano 
$ nano /etc/postfix/sasl/sasl_passwd

[smtp.gmail.com]:587 correo

Hacemos un mapeo 
$ sudo postmap /etc/postfix/sasl/sasl_passwd
Le damos permiso de escritura y lectura
$ chmod 600 /etc/postfix/sasl/sasl_passwd
$ chmod 600 /etc/postfix/sasl/sasl_passwd.db

$ sudo nano /etc/postfix/main.cf

relayhost = [smtp.gmail.com]:587

smtp_sasl_auth_enable = yes
smtp_sasl_security_options = noanonymous
smtp_sasl_password_maps = hash:/etc/postfix/sasl/sasl_passwd
smtp_tls_security_level = encrypt
smtp_tls_CAfile = /etc/ssl/certs/ca-certificates.crt

Pasa mos a instalar
$ sudo apt install multiutils -y

Reiniciamos 
Systemctl restart postifix 
Systemctl status postfix 

Pasa mos a instalar
$ sudo apt install multiutils -y

Vamos a mandarnos un correo 
Echo “correo de prueba” | mail -s “correo de prueba” angelsantan5657@gmail.com

Practica 3: Instalar un servidor de Impresion (1pts)

sudo apt install cups
sudo apt install cups-pdf
systemctl start cups

Navegador: localhost:631

sudo ufw allow 631/tcp
sudo /usr/sbin/cupsctl --remote-admin --remote-any --share-printers
systemctl restart cups
systemctl restart ufw

(administration > add printer > 
whoami
cups-pdf
check share this printer
generic
cups pdf no options
add printer)

set printer options
hostname -I
"ip":631 desde pc host
