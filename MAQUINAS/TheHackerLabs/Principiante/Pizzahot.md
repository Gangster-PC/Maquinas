Escaneo de puertos:
![[Pasted image 20240712172937.png]]

Veamos lo que hay en el puerto 80:
![[Pasted image 20240712173222.png]]
Tenemos una pagina de venta de pizza común y corriente 

Veamos lo que hay en su codigo fuente (Control+U)
![[Pasted image 20240712174147.png]]
Tenemos un posible usuario llamado pizzapiña

Haremos un ataque de fuerza bruta con Hydra a este usuario por el puerto 22, para saber su contraseña
![[Pasted image 20240712174512.png]]
Y efectivamente nos arroja que es steven su contraseña

Haremos la intrusión por medio del puerto SSH
![[Pasted image 20240712174551.png]]
Estamos dentro

La flag del user es:
![[Pasted image 20240712174625.png]]

## ESCALADA DE PRIVILEGIOS

Ejecutamos sudo -l para ver el binario que podremos usar 
![[Pasted image 20240712174721.png]]
Y vemos que para ser el usuario Pizzasinpiña podemos ejecutar el binario Gcc

Miramos en GTFOBins como podemos escalar con este binario:
![[Pasted image 20240712174810.png]]

Lo ejecutamos:
![[Pasted image 20240712174840.png]]
Y listo ahora somos el usuario Pizzasinpiña

Ejecutamos sudo -l para ver el binario que podremos usar para ser root
![[Pasted image 20240712174915.png]]
Podemos usar el binario Man para hacer la escalada a root

Miramos en GTFOBins como podemos escalar con este binario:
![[Pasted image 20240712175006.png]]

Lo ejecutamos:
![[Pasted image 20240712175103.png]]
![[Pasted image 20240712175255.png]]
![[Pasted image 20240712175327.png]]
Y listo, ya somos root

Y la flag de root:
![[Pasted image 20240712175353.png]]
