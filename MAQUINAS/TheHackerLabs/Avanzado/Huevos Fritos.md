Escaneo de puertos:
![[Pasted image 20240812091457.png]]

Veamos lo que hay en el puerto 80:
![[Pasted image 20240812091533.png]]
Tenemos una platilla de Apache

Haremos fuzzing web para encontrar directorios con Gobuster:
![[Pasted image 20240812091706.png]]
Encontramos el directorio /squirting

Accedamos a él:
![[Pasted image 20240812091735.png]]
Tenemos un panel de login y una parte para subir archivos

Intentamos acceder con usuario admin y la contraseña admin y subir una reverse shell en PHTML, por ejemplo
![[Pasted image 20240812092341.png]]
![[Pasted image 20240812092833.png]]
Y nos sale:
![[Pasted image 20240812092848.png]]
Que el tipo de archivo no es permitido

Abriré Burpsuite para interceptar la petición y lograr decifrar que archivos acepta este panel de subida de archivos:
![[Pasted image 20240812093108.png]]
Mandamos todo al Intruder:
![[Pasted image 20240812093223.png]]
Señalamos la parte en la que vamos a probar varios tipos de extensiones para ver cual nos acepta la web:
![[Pasted image 20240812093335.png]]
Creamos una lista con posibles extensiones .PHP:
![[Pasted image 20240812093810.png]]
Y damos al botón naranja de Start Attack:
![[Pasted image 20240812094004.png]]
Y obsevamos que unicamente acepta las extensiones .phar

Cambiamos nuestro archivo de la reverse shell a .phar y lo intentamos subir nuevamente:
![[Pasted image 20240812094129.png]]
![[Pasted image 20240812094143.png]]
Listo, ahora si se subió nuestro archivo satisfactoriamente

Veamos el código fuente de esta página:
![[Pasted image 20240812092121.png]]
Tenemos un posible directorio

Intentemos acceder a él:
![[Pasted image 20240812094233.png]]
Encontramos nuestro archivo

Nos ponemos a la escucha con NetCat damos click en nuestro archivo:
![[Pasted image 20240812094313.png]]
Y estamos dentro de la máquina:

Hacemos tratamiento de la TTY:
![[Pasted image 20240812094458.png]]
![[Pasted image 20240812094519.png]]
## ESCALADA DE PRIVILEGIOS

En el directorio /var/backup nos encontramos con un archivo escondido:
![[Pasted image 20240812094801.png]]
Llamado .cositas

Lo leemos:
![[Pasted image 20240812094823.png]]
Tenemos una id_rsa

Veamos los usuarios que contiene esta máquina:
![[Pasted image 20240812094850.png]]
Tenemos el usuario huevos fritos

Nos pasamos esta id_rsa a nuestro kali
![[Pasted image 20240812094940.png]]

Extraemos el hash de este id_rsa con Ssh2john:
![[Pasted image 20240812095152.png]]

Y lo crackeo con John, para saber su contraseña:
![[Pasted image 20240812095437.png]]
Y es honda1:

Le damos permisos a el id_rsa y accedemos por el puerto 22 SSH:
![[Pasted image 20240812095518.png]]
Y listo, estamos nuevamente dentro de la máquina pero ahora siendo otro usuario

Flag de user:
![[Pasted image 20240812095559.png]]

Ejecutamos sudo -l para ver el binario que podremos usar 
![[Pasted image 20240812095638.png]]
Podemos ser root con el binario Python

Miramos en GTFOBins como podemos escalar con este binario:
![[Pasted image 20240812095759.png]]

Crearemos un archivo .py:
![[Pasted image 20240812100154.png]]

Ahora ejecutaremos este archivo root.py con el binario python3:
![[Pasted image 20240812100236.png]]
Y listo, ya somos  ROOT

Flag de root:
![[Pasted image 20240812100315.png]]







