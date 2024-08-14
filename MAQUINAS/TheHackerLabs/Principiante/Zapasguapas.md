Escaneo de puertos:
![[Pasted image 20240807094351.png]]

Veamos lo que hay en el puerto 80:
![[Pasted image 20240807094453.png]]
Es una página de venta de zapatillas

Haremos fuzzing web con Gobuster en busca de directorios
![[Pasted image 20240807095616.png]]
Encontramos un /login.html

Accedamos a él:
![[Pasted image 20240807095916.png]]

Probemos meter admin como usuario y contraseña a ver que sale:
![[Pasted image 20240807095951.png]]
![[Pasted image 20240807095958.png]]
Nos aparece nada, página en blanco

Probaremos meter un comando en ambos campos, por ejemplo whoami
![[Pasted image 20240807100046.png]]
![[Pasted image 20240807100052.png]]
Y efectivamente la maquina nos responde al comando que le pedimos

Le escribiremos una reverse shell y nos pondremos a la escucha en mi kali para recibir la conexión
![[Pasted image 20240807100237.png]]
![[Pasted image 20240807100302.png]]
Y listo, recibimos la conexión y ahora estamos dentro de la máquina

Tratamiento de la tty:
![[Pasted image 20240807100344.png]]
![[Pasted image 20240807100404.png]]

## ESCALADA DE PRIVILEGIOS

En el directorio /home/pronike encontramos una nota.txt, veamos lo que contiene:
![[Pasted image 20240807100534.png]]
Tenemos un posible usuario llamado proadidas

Aunque revisando en el directorio /opt encotramos un archivo .zip
![[Pasted image 20240807100641.png]]

Convertiré el .zip a base64:
![[Pasted image 20240807101428.png]]

Y en mi kali crearé un archivo .zip con este archivo base 64:
![[Pasted image 20240807101800.png]]

Ahora le sacaré el hash con Zip2john y despues crackearemos esta hash con John:
![[Pasted image 20240807101844.png]]
La contraseña para poder descomprimir el archivo importante.zip es hotstuff

Descomprimir:
![[Pasted image 20240807101932.png]]
Leamos el password.txt que extraímos:
![[Pasted image 20240807102011.png]]
Tenemos la contraseña de pronike

Escalemos al usuario pronike con estas credenciales:
![[Pasted image 20240807102103.png]]
Listo, ya somos el usuario pronike

Ejecutamos sudo -l para ver el binario que podremos usar 
![[Pasted image 20240807102157.png]]
Podemos ser el usuario proadidas con el binario Apt

Miramos en GTFOBins como podemos escalar con este binario:
![[Pasted image 20240807102340.png]]

Lo ejecutamos:
![[Pasted image 20240807102404.png]]
![[Pasted image 20240807102427.png]]
![[Pasted image 20240807102439.png]]
Y listo, ya somos el usuario proadidas

Ejecutamos sudo -l para ver el binario que podremos usar 
![[Pasted image 20240807102522.png]]
Podemos ser root con el binario Aws

Miramos en GTFOBins como podemos escalar con este binario:
![[Pasted image 20240807102612.png]]

Lo ejecutamos:
![[Pasted image 20240807102743.png]]
![[Pasted image 20240807102814.png]]
![[Pasted image 20240807102830.png]]
Y listo, ya somos ROOT

Flag de user:
![[Pasted image 20240807102857.png]]

Flag de root:
![[Pasted image 20240807102910.png]]
