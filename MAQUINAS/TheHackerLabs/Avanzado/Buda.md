Escaneo de puertos:
![[Pasted image 20240812104438.png]]

Veamos lo que hay en el puerto 80:
![[Pasted image 20240812104455.png]]
Tenemos una plantilla de Apache

Haremos fuzzing web con Gobuster para encontrar direcotorios:
![[Pasted image 20240812104656.png]]
Encontramos el directorio /robots.txt

Accedamos a el:
![[Pasted image 20240812104746.png]]
Metamos este dominio a nuestro /etc/hosts:
![[Pasted image 20240812104856.png]]

Y accedemos a esa página:
![[Pasted image 20240812105018.png]]
Tenemos una especie de cuenta regresiva

Haremos fuzzing web con Wfuzz para encontrar sub-dominios:
![[Pasted image 20240812110310.png]]
Y encontramos el subdominio dev

Accedamos a esta nueva dirección web:
![[Pasted image 20240812110413.png]]
Tenemos un panel de login

Intentemos hacer una inyeccón SQL:
![[Pasted image 20240812110540.png]]
![[Pasted image 20240812110605.png]]
Y si, si es vulnerable a inyección SQL

Vamos a hacer una inyección SQL con ayuda de la herramienta Sqlmap:
1. Enumeraremos posibles bases de datos
```
sqlmap --url http://dev.budasec.thl --dbs --batch --forms  
```
![[Pasted image 20240812111103.png]]
![[Pasted image 20240812110910.png]]
Usaré la base de datos buda
2. Enumeraremos posibles tablas, de esta base de datos:
![[Pasted image 20240812111130.png]]
![[Pasted image 20240812111002.png]]
Tenemos la tabla llamada Users
3. Enumeraremos posibles columnas de esta tabla:
![[Pasted image 20240812111224.png]]
![[Pasted image 20240812111238.png]]
Tenemos 4 columnas hashed_password, id, password y username

4. Y por último, enumeraremos usuarios de estas 4 columnas:
![[Pasted image 20240812111553.png]]
![[Pasted image 20240812111616.png]]

Intentamos acceder al puerto FTP 21 con la primera credencial de username y password:
![[Pasted image 20240812111913.png]]
Y listo, estamos dentro de el puerto 21

Tratamos de ver el contenido del puerto:
![[Pasted image 20240812112020.png]]
Pero hay un Firewall que nos impide leer los archivos 

La solución es: 
![[Pasted image 20240812112204.png]]
Tenemos una carpeta llamada ftp

Accedemos a esta carpeta:
![[Pasted image 20240812112308.png]]
Nos descargamos todo de la carpeta documents con el comando mget *:
![[Pasted image 20240812112900.png]]

Revisemos el knock
![[Pasted image 20240812113118.png]]
Tenemos varios numeros de puertos

Haremos golpeo de puertos:
![[Pasted image 20240812113436.png]]

Y hacemos nuevamente escaneo de puertos con Nmap:
![[Pasted image 20240812113551.png]]
Y evidenciamos que ahora se abrió el puerto 22 SSH

Uno de los documentos que descargamos del puerto 21 fue un .zip, le extraeremos el hash con Zip2john y lo crackeamos con John:
![[Pasted image 20240812113820.png]]
Y la contraseña del .zip es manuelito. Lo extraemos el .zip y nos saca un archivo llamado audit2024

Lo leemos este archivo extraido:
![[Pasted image 20240812113916.png]]
Es una auditoria

Pero lo que más me llama la atención de este documento son estas credenciales:
![[Pasted image 20240812114724.png]]

Probamos con estas credenciales entrar por el puerto SSH:
![[Pasted image 20240812114247.png]]
![[Pasted image 20240812114306.png]]
Y listo, estamos dentro de la máquina

Flag de user:
![[Pasted image 20240812114322.png]]

## ESCALADA DE PRIVILEGIOS

Escribimos id para ver los grupos en los cuales pertenecemos siendo este usuario:
![[Pasted image 20240812115045.png]]
Pertenecemos a el grupo docker tambien

Miramos en GTFObins como podemos ser root con esta Shell de docker:
![[Pasted image 20240812115132.png]]

Lo ejecutamos:
![[Pasted image 20240812115155.png]]

Pero revisando, estamos dentro del contenedor de docker:
![[Pasted image 20240812115449.png]]
Entonces editamos el archivo /etc/passwd y borramos la X de root:
![[Pasted image 20240812115524.png]]
![[Pasted image 20240812115535.png]]
![[Pasted image 20240812115624.png]]
Y listo, ahora si somos usuarios ROOT

Flag de root:
![[Pasted image 20240812115220.png]]


