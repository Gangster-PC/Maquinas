Escaneo de puertos:
![[Pasted image 20240805074823.png]]

Veamos lo que hay en el puerto 80:
![[Pasted image 20240805074844.png]]
Tenemos una plantilla de apache

Revisando su código fuente encontré:
![[Pasted image 20240805074924.png]]
En la línea 213 tenemos un código cifrado en Brainfuck

Lo deciframos:
![[Pasted image 20240805075117.png]]
Y tenemos una posible contraseña llamada "abuelacalientalasopa"

Así que probamos acceder al puerto 22 con el usuario abuela y la contraseña ya descifrada 
![[Pasted image 20240805075828.png]]
Y estamos dentro de la máquina

## ESCALADA DE PRIVILEGIOS

Ejecutamos sudo -l para ver el binario que podremos usar 
![[Pasted image 20240805075959.png]]
Podemos ser root con el binario Node

Miramos en GTFOBins como podemos escalar con este binario:
![[Pasted image 20240805080040.png]]

Lo ejecutamos:
![[Pasted image 20240805080149.png]]
Y listo, ya somos ROOT

Flag de user:
![[Pasted image 20240805080215.png]]

Flag de root:
![[Pasted image 20240805080308.png]]



