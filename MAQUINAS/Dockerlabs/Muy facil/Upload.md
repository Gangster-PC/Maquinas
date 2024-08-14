Escaneo de puertos:
![[Pasted image 20240705201619.png]]

En el puerto 80 tenemos:
![[Pasted image 20240705201708.png]]
Una subida de archivos

Procedemos a subir un archivo .php con una reverse shell hacia nuestra maquina Linux
![[Pasted image 20240705201856.png]]

Ahora hacemos un fuzzing web con Gobuster para encontrar el archivo que acabamos de subir
![[Pasted image 20240705202001.png]]

Lo encontramos está ubicado en /uploads
![[Pasted image 20240705202042.png]]

Nos ponemos a la escucha con netcat por el puerto 443 y damos click en el archivo shell.php y recibimos la shell reversa
![[Pasted image 20240705202216.png]]

Hacemos tratamiento de la TTY
![[Pasted image 20240705202527.png]]
![[Pasted image 20240705202604.png]]

## ESCALADA DE PRIVILEGIOS

Ejecutamos sudo -l para ver el binario que podremos usar 
![[Pasted image 20240705202648.png]]
Podemos ser root con el binario env

Miramos en GTFOBins como podemos escalar con este binario:
![[Pasted image 20240705203427.png]]

Lo ejecutamos:
![[Pasted image 20240705202830.png]]

Y listo, ya somos usuario ROOT 




