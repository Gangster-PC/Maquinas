Escaneo de puertos:
![[Pasted image 20240805160312.png]]

Veamos lo que hay en el puerto 80:
![[Pasted image 20240805160404.png]]
Tenemos una plantilla de Apache

Revisando el código fuente de esta página web nos encontramos con un usuario
![[Pasted image 20240805160458.png]]
Llamado Melanie

Así que haremos fuerza bruta con Hydra al puerto SSH con este usuario para encontrar su contraseña:
![[Pasted image 20240805160920.png]]
Y encontramos que la contraseña para el usuario melanie es trustno1

Intrusión al puerto SSH
![[Pasted image 20240805161017.png]]
Estamos dentro de la máquina

Flag de user:
![[Pasted image 20240805161040.png]]

## ESCALADA DE PRIVILEGIOS

Ejecutamos sudo -l para ver el binario que podremos usar 
![[Pasted image 20240805161109.png]]
Podemos ser root con el binario Puttygen

Genero 2 claves ssh, una pública y una privada
![[Pasted image 20240805162009.png]]
![[Pasted image 20240805162028.png]]

Ahora explotamos la clave pública:
![[Pasted image 20240805162131.png]]
```
sudo /usr/bin/puttygen id_rsa.pub -O public-openssh -o /root/.ssh/authorized_keys
```

Y accedemos a la maquina siendo root sin proporcionar contraseña por medio de SSH:
![[Pasted image 20240805162325.png]]
Y listo, entramos a la máquina siendo usuario ROOT

Flag de root:
![[Pasted image 20240805162403.png]]
