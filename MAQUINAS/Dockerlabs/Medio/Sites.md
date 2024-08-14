Escaneo de puertos:
![[Pasted image 20240806085707.png]]

Veamos lo que hay en el puerto 80:
![[Pasted image 20240806090023.png]]
Tenemos una especie de manual para poder proteger un Apache y su configuración, pero también la página nos da una pista de usar LFI (Local File Inclusion) entonces usaremos esta pista para poder leer directorios internos de la máquina sin acceder directamente a ella

Haremos fuzzing web en busca de directorios con Gobuster
![[Pasted image 20240806090252.png]]
Encontramos /vulnerable.php

Accedamos a el:
![[Pasted image 20240806090323.png]]

Hagamos el Local File Inclusion apuntando hacia el directorio /etc/passwd para ver los usuarios que contiene la máquina:
![[Pasted image 20240806090427.png]]
Usaremos la herramienta Wfuzz para encontrar la palabra clave que va en FUZZ para poder acceder a la carpeta de passwd
![[Pasted image 20240806090513.png]]
Y la palabra clave es Page

Accedemos ahora si a leer el contenido de esta carpeta:
![[Pasted image 20240806091011.png]]
Y encontramos un usuario llamado chocolate

En la pagina web se menciona un archivo llamado sitio.conf el cual contiene información sensible, vamos a encontrarlo:
![[Pasted image 20240806092456.png]]
Nos encontramos en él que existe un archivo llamado archivitotraviesito

Vamos a encontrarlo:
![[Pasted image 20240806092613.png]]
Lo encontramos, y contiene la contraseña del usuario chocolate

Intrusión al puerto 22:
![[Pasted image 20240806092705.png]]
Y listo, estamos dentro de la máquina

## ESCALADA DE PRIVILEGIOS

Ejecutamos sudo -l para ver el binario que podremos usar
![[Pasted image 20240806092742.png]]
Podemos ser root con el binario Sed

Miramos en GTFOBins como podemos escalar con este binario:
![[Pasted image 20240806092832.png]]

Lo ejecutamos:
![[Pasted image 20240806092908.png]]

Y listo, ya somos ROOT