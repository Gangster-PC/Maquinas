Escaneo de puertos:
![[Pasted image 20240804172737.png]]

Veamos lo que hay en el puerto 1000
![[Pasted image 20240804173023.png]]
Un panel de login de Webmin el cual no tenemos ni usuario ni contraseña

Veamos que exploit encontramos en Metasploit para este Webmin
![[Pasted image 20240804173307.png]]

Usaremos el 10 y veremos los datos que nos pide el exploit:
![[Pasted image 20240804173448.png]]

Nos pide RHOST y LHOST:
![[Pasted image 20240804173616.png]]

Y escribimos run
![[Pasted image 20240804173703.png]]

Y ya estamos dentro de la máquina

La flag de user: 
![[Pasted image 20240804173829.png]]
## ESCALADA DE PRIVILEGIOS

Ejecutamos getcap -r / para ver los binarios que podemos usar 
![[Pasted image 20240804174933.png]]
Tenemos el binario Gdb 

Miramos en GTFOBins como podemos escalar con este binario:
![[Pasted image 20240804180202.png]]

Y lo ejecutamos:
![[Pasted image 20240804180146.png]]

Y listo, ya somos ROOT

La flag de root:
![[Pasted image 20240804180250.png]]
