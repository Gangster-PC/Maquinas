Escaneo de puertos:
![[Pasted image 20240801181031.png]]
![[Pasted image 20240801181054.png]]

Tenemos el puerto 21 FTP abierto, veamos lo que contiene
![[Pasted image 20240801181357.png]]

Nos descargamos el ayuda.txt 
![[Pasted image 20240801181447.png]]

Y lo leemos:
![[Pasted image 20240801181511.png]]
Tenemos un usuario llamado Geralt, pero nos dice que la contraseña la encontraremos con fuerza bruta y que contiene 5 carácteres empieza por P y termina por A

Crearemos este diccionario con la herramienta Crunch tal y como nos lo piden:
![[Pasted image 20240802185011.png]]
![[Pasted image 20240802185034.png]]

Veamos lo que hay en el puerto 8080
![[Pasted image 20240801181635.png]]
Tenemos un panel de login de la plataforma Jenkins

Haremos un ataque de fuerza bruta con la herramienta Patator con el usuario de geralt a este panel de login web de Jenkins usando el diccionario.txt 
![[Pasted image 20240802184826.png]]
Y nos encuentra que la contraseña para el usuario geralt es panda

Accedemos a Jenkins:
![[Pasted image 20240802185205.png]]
Estamos dentro de la plataforma

Vamos a Manage Jenkins
![[Pasted image 20240802185314.png]]

Y bajamos y damos click en Script Console
![[Pasted image 20240802185425.png]]

Y le pasamos una reverse shell en el lenguaje de Groovy
![[Pasted image 20240802185519.png]]

Nos podemos a la escucha con Netcat y damos click en Run
![[Pasted image 20240802185908.png]]
Y tenemos conexión, estamos dentro de la maquina

Intento ser geralt con la misma contraseña del panel de login de Jenkins
![[Pasted image 20240802190042.png]]
Y ahora soy geralt

La flag de user:
![[Pasted image 20240802190119.png]]

## ESCALADA DE PRIVILEGIOS

Observamos los binarios de la máquina:
![[Pasted image 20240802190221.png]]
Y evidenciamos que podemos escalara a root con el binario Php

Miramos en GTFOBins como podemos escalar con este binario:
![[Pasted image 20240802190406.png]]

Lo ejecutamos:
![[Pasted image 20240802190724.png]]
Y listo ya somos ROOT

La flag de root:
![[Pasted image 20240802190909.png]]


