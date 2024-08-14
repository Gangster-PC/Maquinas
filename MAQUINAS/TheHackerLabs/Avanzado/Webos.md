Escaneo de puertos:
![[Pasted image 20240808160507.png]]

Veamos lo que hay en el puerto 80:
![[Pasted image 20240808160539.png]]

Tenemos un panel de Login, probamos metiendo admin en ambos campos:
![[Pasted image 20240808160823.png]]
Y al parecer era una plantilla de login falso, ahora si accedimos a un panel de login verdadero de la página Grav

Usamos Rpcclient para ver los usuarios q tiene esta máquina:
![[Pasted image 20240808162038.png]]
Y encontramos q tiene el usuario "webos"

Con Smbclient encontramos una carpeta compartida la cual se llama webos
![[Pasted image 20240808162118.png]]

Intentamos acceder a ella con el usuario webos, anteriormente encontrado:
![[Pasted image 20240808162146.png]]
Pero nos pide la contraseña de este usuario la cual no tenemos todavia

Usamos fuerza bruta con Medusa para encontrar la contraseña de este usuario:
![[Pasted image 20240808164121.png]]
```
medusa -h 192.168.1.206 -u webos -P /usr/share/wordlists/rockyou.txt -M smbnt
```
Y nos encontró que la contraseña es:
![[Pasted image 20240808164303.png]]
Geraldine

Accedamos a la máquina por el puerto 445 con estas credenciales para ver que nos encontramos:
![[Pasted image 20240808164430.png]]
Nos encontramos con un .txt

Lo pasamos a nuestro kali para leerlo:
![[Pasted image 20240808164553.png]]
Y tenemos un mensaje codificado en Brainfuck 

Lo decodificamos:
![[Pasted image 20240808164647.png]]
Y nos encontramos con unas credenciales, admin:Perico69*****

Las probamos en la página web:
![[Pasted image 20240808164746.png]]
![[Pasted image 20240808164755.png]]
Y, efectivamente logramos acceder a la página web

Como no logramos ver nada importante o un boton, haremos fuzzing web con Gobuster en busca de directorios:
![[Pasted image 20240808165202.png]]
Nos encuentra bastantes, pero el que nos interesa se llama /admin

Accedamos al directorio /admin:
![[Pasted image 20240808165249.png]]
Tenemos un panel de login nuevamente, probemos con las credenciales ya encontradas anteriormente:
![[Pasted image 20240808165324.png]]
![[Pasted image 20240808165336.png]]
Y ahora si logramos acceder satisfactoriamente a la pagina web de Grav

Obsevamos que tenemos la versión 1.7.44 de Grav
![[Pasted image 20240808165645.png]]

Buscaré un exploit en internet para poder ejecutarlo:
![[Pasted image 20240808170117.png]]
Encontré ese

Así que procedo a descargarlo en mi kali:
![[Pasted image 20240808170156.png]]

Pero antes de ejecutar el graver.py primero lo edito con mis credenciales de acceso:
![[Pasted image 20240808170506.png]]

Ahora si ejecuto el graver.py:
![[Pasted image 20240808170544.png]]

Vamos a la dirección que nos dice el exploit:
![[Pasted image 20240808170612.png]]
Y lo que hace el exploit es crearnos un LFI 

Vamos a la pestaña Páginas y despues a hacked:
![[Pasted image 20240808171042.png]]
![[Pasted image 20240808171106.png]]
Acá podemos poner un comando y si le damos al ojito al lado derecho de la página nos muestra el resultado
![[Pasted image 20240808171134.png]]
Ejemplo con el comando whoami:
![[Pasted image 20240808171156.png]]

Entonces le coloco una revshel, le doy al boton del ojito y me pongo a la escucha con Netcat:
![[Pasted image 20240808171344.png]]
![[Pasted image 20240808171357.png]]
Y recibo la conexión, ahora estoy dentro de la máquina

Tratamiento de la tty:
![[Pasted image 20240808171442.png]]
![[Pasted image 20240808171509.png]]

## ESCALADA DE PRIVILEGIOS

Revisando el directorio /opt tenemos una id_rsa
![[Pasted image 20240808171839.png]]

Me la paso a mi kali y le extraigo la hash con Ssh2john y la crackeo con John
![[Pasted image 20240808171947.png]]
![[Pasted image 20240808172418.png]]
Encontramos la contraseña del id_rsa

Buscamos que usuarios tenemos:
![[Pasted image 20240808172510.png]]

Así que usaremos esta id_rsa para entrar por el puerto SSH con el usuario webos y la contraseña freestyle![[Pasted image 20240808172642.png]]
Y estamos dentro de la máquina nuevamente pero ahora desde el puerto 22

Flag de user:
![[Pasted image 20240808172746.png]]

Para ser usuarios root, observemos las capabilities que tiene la máquina
![[Pasted image 20240808173331.png]]
Y encontramos que tiene la capabilitie de Python3 descargada el la dirección /home/webos

Miramos en GTFObins como escalar con python
![[Pasted image 20240808173105.png]]

Lo ejecutamos:
![[Pasted image 20240808173130.png]]
Y listo, ya somos ROOT

Flag de root:
![[Pasted image 20240808173156.png]]
