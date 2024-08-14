Escaneo de puertos:
![[Pasted image 20240729191148.png]]

Veamos lo que hay en el puerto 80:
![[Pasted image 20240729191501.png]]

Intenté hacer fuzzing web y no encontré nada los botones de la pagina no me llevan a ningún lado, simplemente se recarga la pagina 

Así que abriré Burpsuite para ver como se tramita la petición de los botones
![[Pasted image 20240729191647.png]]
![[Pasted image 20240729192552.png]]
Damos click en Submit Reservation
![[Pasted image 20240729192626.png]]
Y se nos abre Burpsuite con la petición interceptada

Mandamos todo al Repeater
![[Pasted image 20240729192727.png]]

Probamos metiendo otra palabra en userInput y vemos que nos dice que acepta base64
![[Pasted image 20240729192824.png]]

Leeremos el archivo /etc/passwd pero con un comando en base 64
![[Pasted image 20240729192931.png]]
![[Pasted image 20240729193040.png]]
Tenemos el usuario cachopin

Haremos un ataque de fuerza bruta al puerto SSH con este usuario para saber su contraseña:
![[Pasted image 20240729193242.png]]
Y encontramos que es "simple"

Haremos la intrusión al puerto 22:
![[Pasted image 20240729193331.png]]
Y listo, estamos dentro

## ESCALADA DE PRIVILEGIOS 

En el directorio /home/cachopin/app/com/personal tenemos un archivo llamado hash.lst con diferentes hashes
![[Pasted image 20240729193624.png]]

Nos descargamos la  herramienta de PatxaSec llamada SHA_Decrypt para decifrar la contraseña de estas hashes 
![[Pasted image 20240729195942.png]]
![[Pasted image 20240729200009.png]]

Probamos con la primera hash:
![[Pasted image 20240729200357.png]]
Y con la primera no nos encontró nada

Probaremos con la segunda:
![[Pasted image 20240729200453.png]]
Encontramos cecina, que es la contraseña de root

Intentamos ser root con esta contraseña:
![[Pasted image 20240729200540.png]]
Y listo, ya somos ROOT
