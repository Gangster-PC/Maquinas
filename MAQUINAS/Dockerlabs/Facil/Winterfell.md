Escaneo de puertos:
![[Pasted image 20240722183638.png]]
Vemos que es una máquina Windows debido a que tiene los puertos 139 y 445 abiertos, Samba

Veamos lo que hay en el puerto 80:
![[Pasted image 20240722183802.png]]
Tenemos unos posibles usuarios o contraseñas

Haremos fuzzing web con Gobuster para encontrar dominios:
![[Pasted image 20240722183921.png]]

Tenemos un /dragon, veamos lo que hay en el:
![[Pasted image 20240722183957.png]]
Un archivo "EpisodiosT1", que contiene:
![[Pasted image 20240722184033.png]]
Mas posibles usuarios o contraseñas

Meteremos todos los posibles usuarios o contraseñas encontrados en las anteriores 2 paginás en un .txt:
![[Pasted image 20240722184143.png]]

Ahora con este archivo de texto haremos fuerza bruta con la herramienta Crackmapexec para entrar por el puerto 445 y leer posibles carpetas:
![[Pasted image 20240722184309.png]]
Encontramos el usuario jon con su contraseña seacercaelinvierno

Buscaremos carpetas dentro de esta maquina con Smbclient:
![[Pasted image 20240722184429.png]]
Y encontramos la carpeta shared

Entraremos a la maquina con las credenciales encontradas anteriormente y veremos lo que hay en este directorio:
![[Pasted image 20240722184533.png]]
Tenemos un "proteccion_del_reino"

Nos lo descargamos para ver que contiene:
![[Pasted image 20240722184612.png]]

Y lo leemos desde nuestra máquina:
![[Pasted image 20240722184638.png]]
Tenemos un mensaje de Jon hacia Aria dándole una contraseña pero en base 64
![[Pasted image 20240722184819.png]]
Y al decodificarlo tenemos "hijodelanister"

Haremos la intrusión con el usuario jon y la contraseña hijodelanister, por el puerto 22:
![[Pasted image 20240722184920.png]]
Y estamos dentro de la máquina ahora si

## ESCALADA DE PRIVILEGIOS

Ejecutamos sudo -l para ver el binario que podremos usar 
![[Pasted image 20240722184957.png]]
Vemos que podemos ser el usuario Aria ejecutando un script en python llamado .mensaje.py ubicado en el directorio de jon

Veamos lo que contiene el .mensaje.py
![[Pasted image 20240722185139.png]]
Es un script que encripta un mensaje introducido por el usuario, pero también se puede observar que usa una librería llamada Hashlib, la cual tiene una vulnerabilidad

Creamos un archivo llamado hashlib.py con una bash:
![[Pasted image 20240722185402.png]]

Ahora hacemos que el script de .mensaje.py lea nuestro archivo malicioso para así poder ser el usuario Aria:
![[Pasted image 20240722185519.png]]
Y listo ya somos aria

Ejecutamos sudo -l para ver el binario que podremos usar 
![[Pasted image 20240722185613.png]]
Observamos que con el usuario daenerys podemos leer y listar archivos

Observamos que en el directorio de daenerys tenemos un archivo:
![[Pasted image 20240722185737.png]]

Procedemos a leerlo para ver que dice:
![[Pasted image 20240722185814.png]]
Tenemos una posible contraseña que sería "drakaris"

Ahora intentaremos ser el usuario daenerys con la contraseña drakaris
![[Pasted image 20240722185913.png]]
Listo ya somos daenerys

Ejecutamos sudo -l para ver el binario que podremos usar 
![[Pasted image 20240722190017.png]]
Podemos ser usuario root con el binario bash leyendo un archivo .shell.sh

Así que lo ejecutaremos:
![[Pasted image 20240722190145.png]]

Leeremos ahora los binarios de la máquina y ahora tenemos un /bin/bash
![[Pasted image 20240722190222.png]]

Ejecutaremos el comando bash -p:
![[Pasted image 20240722190249.png]]
Y listo, ya somos ROOT

