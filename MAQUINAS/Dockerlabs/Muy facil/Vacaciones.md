Escaneo de puertos:
![[Pasted image 20240707200817.png]]

Veamos lo que hay en el puerto 80:
![[Pasted image 20240707200934.png]]
Pagina en blanco

Veamos su codigo fuente:
![[Pasted image 20240707201006.png]]
Tenemos 2 posibles usuarios Juan y Camilo

Creamos un archivo de texto con estos 2 usuarios
![[Pasted image 20240707201151.png]]


Haremos un ataque de fuerza bruta con Hydra a estos 2 posibles usuarios por medio del puerto 22
![[Pasted image 20240707201248.png]]
Encontramos que el usuario es camilo y su contraseña es password1

Entraremos al puerto SSH con esas credenciales
![[Pasted image 20240707201449.png]]
Estamos dentro

## ESCALADA DE PRIVILEGIOS

Encontramos un correo.txt en la dirreción /var/mail/camilo que dice:
![[Pasted image 20240707201808.png]]

Haremos la intrusión a juan con esa contraseña 
![[Pasted image 20240707201908.png]]
Ahora somos juan

Ejecutamos sudo -l para ver el binario que podremos usar 
![[Pasted image 20240707201945.png]]
Podemos usar el binario ruby para ser root

Miramos en GTFOBins como podemos escalar con este binario:
![[Pasted image 20240707202020.png]]

Lo ejecutamos:
![[Pasted image 20240707202109.png]]

Y listo, ya somos usuarios ROOT 


