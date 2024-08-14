Escaneo de puertos:
![[Pasted image 20240802192828.png]]

Veamos lo que hay en el puerto FTP, ya que está abierto y podemos entrar con el usuario anonymous
![[Pasted image 20240802192908.png]]
Tenemos un secret.txt así que lo descargamos

Leemos lo que contiene:
![[Pasted image 20240802193004.png]]
Nada relevante

Como vimos que podemos acceder al puerto FTP crearé un archivo .php con una RevShell
y lo subiré
![[Pasted image 20240802193211.png]]

Ahora accederemos a este archivo shell.php desde la pagina web y nos pondremos a la escucha con Netcat para recibir la conexión
![[Pasted image 20240802193329.png]]
![[Pasted image 20240802193344.png]]
Y recibimos la conexión

Haremos tratamiento de la TTY:
![[Pasted image 20240802193543.png]]
![[Pasted image 20240802193604.png]]
## ESCALADA DE PRIVILEGIOS

En el directorio /opt encontramos un archivo .txt con algo escrito en lenguaje Brainfuck
![[Pasted image 20240802193803.png]]

Lo desencodeamos:
![[Pasted image 20240802193916.png]]
Y tenemos una posible contraseña cyberpunk2077

Vemos que hay un usuario llamado arasaka
![[Pasted image 20240802194000.png]]

Intentamos ser el usuario arasaka con la contraseña anteriormente descifrada:
![[Pasted image 20240802194052.png]]
Y listo, ahora somos arasaka

La flag de user:
![[Pasted image 20240802194123.png]]

Ejecutamos sudo -l
![[Pasted image 20240802194154.png]]
Y evidenciamos que para poder ser el usuario root podemos ejecutar el archivo randombase64.py con python

Veamos lo que contiene el archivo randombase64.py:
![[Pasted image 20240802194304.png]]
Lo que hace es pedir que ingrese un texto y él lo transforma a base 64
![[Pasted image 20240802194409.png]]

Para ser root haremos lo siguiente con este archivo:

Vemos que el archivo está importando una librería llamada base 64, así que nos crearemos un archivo .py con el mismo nombre pero con un código en python para recibir una /bin/bash:
![[Pasted image 20240802195004.png]]

Ejecutamos el archivo  randombase64.py con python:
![[Pasted image 20240802195059.png]]
Y listo, ya somos ROOT

La flag de root:
![[Pasted image 20240802195140.png]]
