Escaneo de puertos:
![[Pasted image 20240810141916.png]]

Veamos lo que hay en el puerto 80:
![[Pasted image 20240810141949.png]]

Haremos fuzzing web con Wfuzz para encontrar la palabra clave para poder encontrar la carpeta /etc/passd 
![[Pasted image 20240810142849.png]]
La palabra clave es Secret

Accedamos a esta dirección:
![[Pasted image 20240810142927.png]]
![[Pasted image 20240810142938.png]]
Tenemos el usuario luisillo y vaxei

Buscaremos una id_rsa de alguno de los 2 usuarios:
![[Pasted image 20240811112051.png]]
Encontramos el id_rsa de el usuario vaxei

Creamos un archivo con esta id_rsa 
![[Pasted image 20240811112322.png]]

Le damos permisos y accedemos por el puerto 22 con esta id_rsa siendo el usuario vaxei
![[Pasted image 20240811112552.png]]
Y listo, estamos dentro de la máquina

## ESCALADA DE PRIVILEGIOS

Ejecutamos sudo -l para ver el binario que podremos usar 
![[Pasted image 20240811112902.png]]
Para poder ser el usuario luisillo podemos ejecutar el binario Perl

Miramos en GTFOBins como podemos escalar con este binario:
![[Pasted image 20240811112946.png]]

Lo ejecutamos:
![[Pasted image 20240811113022.png]]
Y listo, ya somos el usuario luisillo de la máquina

Ejecutamos sudo -l para ver el binario que podremos usar para seguir escalando privilegios:
![[Pasted image 20240811113116.png]]
Podemos ser root ejecutando con python un archivo ubicado en /opt llamado paw.py

Observemos que hace este archivo .py:
![[Pasted image 20240811113310.png]]
![[Pasted image 20240811113543.png]]
Este script realiza varias tareas sencillas y ejecuta algunos comandos del sistema que solo muestran texto en la terminal. A pesar de incluir funciones que manipulan datos y realizan cálculos, estas no influyen de manera considerable en el resultado final.

Logramos observar que el script importa la librería subprocess, entonces nos crearemos un archivo subprocess.py con una /bin/bash para que al momento de ejecutar el paw.py nos lea nuestro archivo malicioso y automáticamente escalemos a root:
![[Pasted image 20240811114023.png]]
![[Pasted image 20240811114035.png]]

Y listo, ya somos ROOT
