Escaneo de puertos:
![[Pasted image 20240810114718.png]]

Veamos lo que contiene el puerto 80:
![[Pasted image 20240810114706.png]]
Tenemos una imagen de comida

Nos descargamos la imagen para ver si tiene algún documento oculto en ella y rompemos la contraseña con la herramienta de Stegcracker para hacerle Esteganografía a la imagen:
![[Pasted image 20240810120235.png]]
Y encontramos que la contraseña de la imagen es Doogies

Extraemos el documento de la imagen con Steghide y su contraseña:
![[Pasted image 20240810120326.png]]
Tenemos un directorio.txt

Lo leemos:
![[Pasted image 20240810120400.png]]

Accedamos a este directorio:
![[Pasted image 20240810120431.png]]

Nos descargamos el archivo Cocineros:
![[Pasted image 20240810120512.png]]

Pero para lograr leerlo evidenciamos que contiene una contraseña, así que le extraemos la hash con la herramienta Office2john y crackeamos la hash con John:
![[Pasted image 20240810121003.png]]
La contraseña para leer la carpeta Cocineros es horse1

Abrimos el documento con Libreoffice y le proporcionamos la contraseña anteriormente hallada:
![[Pasted image 20240810121456.png]]
![[Pasted image 20240810121512.png]]
Nos encontramos con 3 usuarios

Creamos un archivo con estos 3 usuarios y hacemos un ataque de fuerza bruta con Hydra al puerto SSH:
![[Pasted image 20240810121613.png]]
![[Pasted image 20240810123625.png]]
Y el usuario es carlos y la contraseña es bowwow

Intrusión al puerto 22 SSH con estas credenciales:
![[Pasted image 20240810123704.png]]
Y listo, estamos dentro de la máquina

Flag de user:
![[Pasted image 20240810123738.png]]

## ESCALADA DE PRIVILEGIOS

Ejecutamos sudo -l para ver el binario que podremos usar 
![[Pasted image 20240810123851.png]]
Podemos ser root con el binario Crash

Miramos en GTFOBins como podemos escalar con este binario:
![[Pasted image 20240810123917.png]]

Lo ejecutamos:
![[Pasted image 20240810123936.png]]
![[Pasted image 20240810123953.png]]
![[Pasted image 20240810124005.png]]
Y listo, ya somos ROOT

Flag de root:
![[Pasted image 20240810124039.png]]
