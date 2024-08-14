Escaneo de puertos:
![[Pasted image 20240705194332.png]]

En el puerto 80 tenemos:  

![[Pasted image 20240705194435.png]]

Haciendo fuzzing web  con Gobuster nos encontramos un Secret.php:
![[Pasted image 20240705194549.png]]

En el Secret.php hay:

![[Pasted image 20240705194720.png]]
Dándonos una pista de un usuario llamado Mario

Anteriormente en el escaneo de puertos vimos que estaba abierto el puerto 22 (SSH) entonces le haremos un ataque de fuerza bruta con Hydra con este usuario para encontrar la posible contraseña:
![[Pasted image 20240705194915.png]]
Nos da como usuario mario y contraseña chocolate 

Procedemos a entrar:
![[Pasted image 20240705195012.png]]

## ESCALADA DE PRIVILEGIOS

Ejecutamos sudo -l para ver el binario que podremos usar 
![[Pasted image 20240705195059.png]]
Podemos usar el binario Vim para hacer la escalada a root

Miramos en GTFOBins como podemos escalar con este binario:
![[Pasted image 20240705203729.png]]

Lo ejecutamos:
![[Pasted image 20240705195243.png]]

Y listo ya somos ROOT
