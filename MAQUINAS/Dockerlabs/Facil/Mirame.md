![[Pasted image 20240813092116.png]]
![[Pasted image 20240813092133.png]]
![[Pasted image 20240813092241.png]]
![[Pasted image 20240813092220.png]]
1. Enumeraremos posibles bases de datos
```
sqlmap --url http://172.17.0.2/index.php --dbs --batch --forms
```
![[Pasted image 20240813093627.png]]
![[Pasted image 20240813093707.png]]
Usaré la base de datos Users
2. Enumeraremos posibles tablas, de esta base de datos:
![[Pasted image 20240813093813.png]]
![[Pasted image 20240813093822.png]]
Tenemos la tabla llamada Usuarios
3. Enumeraremos posibles columnas de esta tabla:
![[Pasted image 20240813093851.png]]
![[Pasted image 20240813093906.png]]
Tenemos 3 columnas id, password y username
4. Y por último, enumeraremos usuarios de estas 3 columnas:
![[Pasted image 20240813093942.png]]
![[Pasted image 20240813093951.png]]

Tenemos un posible nombre de directorio llamado "directoriotravieso", así que intentaremos acceder a él a ver si existe:
![[Pasted image 20240813094049.png]]
Efectivamente existe y contiene una imagen

Nos la descargamos y le haremos esteganografía:
![[Pasted image 20240813094230.png]]
Y la contraseña de la imagen para poder extraer sus archivos ocultos es chocolate

La extraemos:
![[Pasted image 20240813094325.png]]
Nos extrae un .zip

Le extraemos la hash con Zip2john y la crackeamos con John:
![[Pasted image 20240813094413.png]]

Extraemos el .zip con la contraseña ya encontrada:
![[Pasted image 20240813094441.png]]
Tenemos un secret.txt

Lo leemos:
![[Pasted image 20240813094459.png]]
Tenemos 2 credenciales 

Intrusión por el puerto 22 SSH con estas credenciales:
![[Pasted image 20240813094547.png]]
Y listo, estamos dentro de la máquina

## ESCALADA DE PRIVILEGIOS

Miramos todos los binarios que contiene la máquina:
![[Pasted image 20240813094802.png]]
Y observamos uno que no es comun, es el binario Find

Miramos en GTFOBins como podemos escalar con este binario:
![[Pasted image 20240813094836.png]]

Lo ejecutamos:
![[Pasted image 20240813094850.png]]

Y listo, ya somos usuarios ROOT

