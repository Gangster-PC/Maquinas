Escaneo de puertos:
![[Pasted image 20240716084029.png]]

Veamos lo que hay en el puerto 80:
![[Pasted image 20240716084110.png]]
Parece una pagina como de una billetera digital

Daremos click en el boton "Get A Quote", para ver su contenido 
![[Pasted image 20240716084439.png]]
Nos pide registrarnos

Me registré con el usuario admin y la contraseña admin123
![[Pasted image 20240716084524.png]]

Ahora iniciare sesión con las credenciales anteriormente mencionadas
![[Pasted image 20240716084602.png]]

Estamos dentro:
![[Pasted image 20240716084624.png]]

Veamos su version de la pagina para encontrar algun exploit
![[Pasted image 20240716084852.png]]
Es Wallos v1.11.0

Veamos que nos encuentra Searchsploit 
![[Pasted image 20240716084959.png]]
Encontramos un .txt, nos lo descargamos y lo leemos
![[Pasted image 20240716085048.png]]
Estos son los pasos que nos dice que debemos seguir, entonces procedemos a realizarlos

1. Loguearnos en la pagina web, que ya lo hicimos anteriormente
2. Ir a una nueva suscripción
![[Pasted image 20240716085209.png]]
3. Subir un .php malicioso, yo lo subiré con una reverse shell:
![[Pasted image 20240716085352.png]]
![[Pasted image 20240716085314.png]]
4. Ahora a este shell.php le agregaremos GIF89a;
![[Pasted image 20240716123233.png]]

Y en la pagina web lo subiremos:
![[Pasted image 20240716123350.png]]

Y daremos en el boton guardar:![[Pasted image 20240716123413.png]]
Si todo nos salió bien debe salir un mensaje de Éxito

Ahora iremos a esta parte de la plataforma para encontrar nuestro shell.php y poder ejecutarlo:
![[Pasted image 20240716123538.png]]
Y aqui lo tendremos 

Ahora nos podemos a la escucha con Netcat y daremos click en mi archivo malicioso para recibir conexión
![[Pasted image 20240716124241.png]]
Y listo tenemos conexión, y de una vez hacemos tratamiento de la TTY

## ESCALADA DE PRIVILEGIOS

Ejecutamos sudo -l para ver el binario que podremos usar 
![[Pasted image 20240716124357.png]]
Vemos que para ser el usuario Pylon podemos ejecutar el binario Awk

Miramos en GTFOBins como podemos escalar con este binario:
![[Pasted image 20240716124550.png]]

Lo ejecutamos:
![[Pasted image 20240716124618.png]]
Y listo, ya somos Pylon

Ahora en la dirección /home/pylon, tenemos un zip
![[Pasted image 20240716124702.png]]
Tratamos de descomprimirlo pero nos pide contraseña, la cual no tenemos

Intetamos levantar un puerto 80 con python para pasarnos este zip a nuestra maquina pero observamos que no tiene python descargado:
![[Pasted image 20240716124804.png]]

Entonces lo que haremos será convertir este .zip en un archivo .zip pero con base 64
![[Pasted image 20240716124837.png]]

Leemos como nos quedo el archivo base64 :
![[Pasted image 20240716124912.png]]

Ahora en nuestra maquina crearemos un archivo .zip con este código:
![[Pasted image 20240716125048.png]]

Y procedemos a hacerle fuerza bruta para sacarle la contraseña al .zip, usando la herramienta Zip2john y John the ripper

Extraemos la hash de clave.zip
![[Pasted image 20240716125541.png]]

Y ahora crackearemos esa hash con John the reapper usando un diccionaro para descubrir la contraseña del .zip
![[Pasted image 20240716125622.png]]

Observamos que la contraseña es chocolate1, entonces descomprimiremos el archivo.zip y veremos lo que tiene dentro:
![[Pasted image 20240716125710.png]]

Tenemos un .txt, veamos lo q dice:
![[Pasted image 20240716125732.png]]
Es la contraseña del usuario Pinguino

Escalaremos ahora a este usuario con su respectiva contraseña
![[Pasted image 20240716125826.png]]
![[Pasted image 20240716125903.png]]
Y listo ya somos Pinguino

Ejecutamos sudo -l para ver con que binario podemos escalar para ser root:
![[Pasted image 20240716125941.png]]
Podemos usar el binario Sed para hacer la escalada a root

Miramos en GTFOBins como podemos escalar con este binario:
![[Pasted image 20240716130039.png]]

Lo ejecutamos:
![[Pasted image 20240716130100.png]]

Y listo, ya somos ROOT








