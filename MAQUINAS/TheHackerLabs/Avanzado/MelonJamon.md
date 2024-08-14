Escaneo de puertos:
![[Pasted image 20240807165317.png]]

Veamos lo que hay en el puerto 80:
![[Pasted image 20240807165330.png]]

Haremos fuzzing web en busca de dierctorios con Gobuster:
![[Pasted image 20240807165516.png]]
Encotramos un directorio llamado /gettingstarted

Accedemos a él:
![[Pasted image 20240807165543.png]]
Tenemos un panel para subir archivos

Revisando su código fuente tenemos:
![[Pasted image 20240807165652.png]]
Un texto codificado en base 64

Decodificación del texto:
![[Pasted image 20240807165736.png]]
Encontramos con yaml que funciona con Python

Buscamos en internet en busca de ayuda y nos encontramos con esta página:
![[Pasted image 20240807170756.png]]
![[Pasted image 20240807170825.png]]

Nos creamos un archivo con este diseño pero le cambiamos para que nos lance una RevShell:
![[Pasted image 20240807171428.png]]

Subo este archivo a la página web y me pongo a la escucha con Netcat:
![[Pasted image 20240807171156.png]]
![[Pasted image 20240807171353.png]]
Y listo, estamos dentro de la máquina

Haremos tratamiento de la tty:
![[Pasted image 20240807171453.png]]
![[Pasted image 20240807171500.png]]
![[Pasted image 20240807171522.png]]

## ESCALADA DE PRIVILEGIOS

Ejecutamos sudo -l para ver el binario que podremos usar 
![[Pasted image 20240807171607.png]]
Podemos ser el usuario melon con el binario Go

Entonces copiamos una reverse shell llamada Golang y nos ponemos a la escucha para recibir la conexión
![[Pasted image 20240807172721.png]]
![[Pasted image 20240807172732.png]]
Nos sale un pequeño error pero no pasa nada
![[Pasted image 20240807172748.png]]
![[Pasted image 20240807172822.png]]
![[Pasted image 20240807172835.png]]
Recibimos la conexión y ahora estamos dentro de la máquina

Flag de user:
![[Pasted image 20240807173000.png]]

Me levanto un servidor con python en el puerto 80 para poder pasarme el Pspy64 a la máquina y ver sus procesos en segundo plano:
![[Pasted image 20240807173310.png]]
![[Pasted image 20240807173337.png]]
Y listo, ya lo tengo en la máquina el programa

Le damos permisos de ejecución al programa y lo ejecutamos ![[Pasted image 20240807173417.png]]
![[Pasted image 20240807173950.png]]
Evidenciamos que está ejecutando el apt update cada cierto tiempo por lo tanto crearé un archivo en esta ruta /etc/apt/apt.conf.d para que le de permisos a la bash y podamos ser root
![[Pasted image 20240807174424.png]]
Y ahora esperamos a que el programa se ejecute
![[Pasted image 20240807174528.png]]
Como ya nos aparece la S en los permisos es que ya está el cambio hecho

Ejecutamos bash -p
![[Pasted image 20240807174607.png]]
Y listo, ya somos ROOT

Flag de root:
![[Pasted image 20240807174629.png]]
