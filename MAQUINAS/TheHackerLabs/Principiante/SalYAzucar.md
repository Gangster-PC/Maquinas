Escaneo de puertos:
![[Pasted image 20240805111838.png]]

Veamos lo que hay en el puerto 80:
![[Pasted image 20240805111818.png]]
Tenemos una plantilla de apache

Haremos fuzzing web con Gobuster en busca de directorios:
![[Pasted image 20240805112004.png]]
Encontramos Summary

Veamos lo que hay en el directorio /summary
![[Pasted image 20240805112232.png]]

Y dentro de summary.html:
![[Pasted image 20240805112251.png]]

Como no encontramos nada de información importante haremos ataque de fuerza bruta con Hydra al puerto SSH al usuario y contraseña:
![[Pasted image 20240805112415.png]]
Encontramos usuario info y contraseña qwerty

Intrusión al puerto 22:
![[Pasted image 20240805112513.png]]
Estamos dentro de la máquina

Flag de user:
![[Pasted image 20240805112605.png]]
## ESCALADA DE PRIVILEGIOS

Ejecutamos sudo -l para ver el binario que podremos usar 
![[Pasted image 20240805112630.png]]
Podemos escalar con el binario Base64 para ser root

Miramos en GTFOBins como podemos escalar con este binario:
![[Pasted image 20240805112721.png]]

Lo ejecutamos:
![[Pasted image 20240805112940.png]]

Nos pasamos el id_rsa de root a nuestro pc 
![[Pasted image 20240805113038.png]]

Le extraemos la hash:
![[Pasted image 20240805113124.png]]

Y la desencriptamos con john de ripper
![[Pasted image 20240805113523.png]]
Y tenemos que es honda1 la contraseña

Entraremos a la maquina nuevamente por el puerto 22 SSH pero ahora siendo root y con ayuda de el archivo id_rsa:
![[Pasted image 20240805113716.png]]
Y listo, accedimos siendo usuarios ROOT

Flag de root:
![[Pasted image 20240805113745.png]]
