Escaneo de puertos:
![[Pasted image 20240708210134.png]]

Veamos lo que hay en el puerto 80:
![[Pasted image 20240708210234.png]]
Tenemos una simple imagen

Nos la descargaremos y le haremos escenografía para ver si depronto tiene algo oculto
![[Pasted image 20240708210329.png]]
Y si, tenemos un usuario llamado borazuwarah

Haremos un ataque de fuerza bruta con Hydra al puerto SSH con este usuario
![[Pasted image 20240708210432.png]]
Su contraseña es 123456

Haremos la intrusión 
![[Pasted image 20240708210522.png]]
Estamos dentro

## ESCALADA DE PRIVILEGIOS

Ejecutamos sudo -l para ver el binario que podremos usar 
![[Pasted image 20240708210551.png]]
Podemos ser root con el binario Bash

Miramos en GTFOBins como podemos escalar con este binario:
![[Pasted image 20240708210732.png]]

Lo ejecutamos:
![[Pasted image 20240708210807.png]]

Y listo ya somos ROOT

