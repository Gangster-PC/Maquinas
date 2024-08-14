Escaneo de puertos:
![[Pasted image 20240804190630.png]]

Veamos lo que hay en el puerto 80:
![[Pasted image 20240804190649.png]]
Tenemos una plantilla de Apache

Haremos fuzzing web para encontrar directorios con la herramienta de Gobuster:
![[Pasted image 20240804190833.png]]
Tenemos un /wordpress
![[Pasted image 20240804191648.png]]
Tenemos una página al parecer hecha en Wordpress

Sigamos haciendo fuzzing pero ahora a este directorio:
![[Pasted image 20240804191020.png]]
Efectivamente estamos frente a un wordpress

Accederemos a /wp-login.php
![[Pasted image 20240804191512.png]]
Tenemos un panel de login 

Usaremos la herramienta Wpscan para ver usuarios:
![[Pasted image 20240804191735.png]]
![[Pasted image 20240804191808.png]]
Tenemos el usuario Dylan

Haremos fuerza bruta para encontrar la contraseña a este usuario con la misma herramienta
![[Pasted image 20240804192043.png]]
![[Pasted image 20240804192112.png]]
La contraseña de dylan es password1

Accedamos a la página con estas credenciales:
![[Pasted image 20240804192201.png]]
![[Pasted image 20240804192313.png]]
Entramos

Ahora vamos a la pestaña Bit File Manager
![[Pasted image 20240804192615.png]]
Luego a wp-content ![[Pasted image 20240804192648.png]]
Ahora Uploads
![[Pasted image 20240804192706.png]]

Ahora nos creamos una RevShell con Msfvenom en un archivo .php
![[Pasted image 20240804192809.png]]

Y lo subimos a la pagina web en la carpeta Uploads
![[Pasted image 20240804192856.png]]

Vamos a la dirección donde subimos este archivo:
![[Pasted image 20240804192931.png]]

Nos ponemos a la escucha con netcat y damos click en nuestro archivo
![[Pasted image 20240804193006.png]]
Y recibimos conexión

Ahora haremos tratamiento de la tty:
![[Pasted image 20240804193158.png]]
![[Pasted image 20240804193220.png]]

## ESCALADA DE PRIVILEGIOS

Nos descargamos Pspy64 que es una herramienta la cual nos deja ver las acciones de la máquina que se están realizando en segundo plano, y le damos permisos de ejecución
![[Pasted image 20240805073446.png]]

Lo ejecutamos y encontramos:
![[Pasted image 20240805073629.png]]
![[Pasted image 20240805073741.png]]
Observamos que se ejecuta un backup.sh en la carpeta /opt en segundo plano

Asi que crearemos este archivo con este nombre y le daremos permisos a la /bin/bash para poder ser usuarios root
![[Pasted image 20240805074135.png]]
Y listo, ya somos ROOT

La flag de user:
![[Pasted image 20240805074253.png]]

La flag de root:
![[Pasted image 20240805074217.png]]
