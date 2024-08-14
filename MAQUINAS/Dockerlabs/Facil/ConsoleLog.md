Escaneo de puertos:
![[Pasted image 20240731191456.png]]

Veamos lo que hay en el puerto 80:
![[Pasted image 20240731191705.png]]
Tenemos una pagina con un boton que en realidad no hace nada

Haremos fuzzing web con la herramienta de Gobuster para encontrar directorios:
![[Pasted image 20240731191817.png]]

Veamos lo que hay en el directorio /backend
![[Pasted image 20240731191856.png]]
Tenemos unos archivos

En el archivo server.js hay:
![[Pasted image 20240731191930.png]]
Encontramos una posible contraseña "lapassworddebackupmaschingonadetodas"

Haremos un ataque de fuerza bruta con Hydra a el puerto 5000 SSH con esta contraseña, para encontrar el usuario:
![[Pasted image 20240731192349.png]]
El usuario es lovely

Intrusión por el puerto 5000 SSH:
![[Pasted image 20240731192446.png]]
Y listo, estamos dentro de la máquina

## ESCALADA DE PRIVILEGIOS

Ejecutamos sudo -l para ver el binario que podremos usar 
![[Pasted image 20240731192607.png]]
Podemos ser root con el binario Nano

Miramos en GTFOBins como podemos escalar con este binario:
![[Pasted image 20240731192652.png]]

Lo ejecutamos:
![[Pasted image 20240731192711.png]]
![[Pasted image 20240731192734.png]]
![[Pasted image 20240731192818.png]]

Y listo, ya somos ROOT




