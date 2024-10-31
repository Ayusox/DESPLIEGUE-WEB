# **Práctica 2.3 - Proxy inverso con Nginx**


## Clonar la máquina virtual

Lo primero que tenemos que hacer es tomar la máquina virtual ya configurada en las prácticas anteriores y la clonamos. 
Tendremos ahora dos máquinas: una que actuará como servidor web y la otra como proxy inverso.

![Descripción de la imagen](images/39.png)

Al clonar, es importante generar una nueva dirección MAC para que ambas máquinas tengan direcciones IP diferentes y no haya conflictos en la red.

![Descripción de la imagen](images/40.png)

## Nginx servidor web

Primero modificamos el archivo de configuración de Nginx en /etc/nginx/sites-available/webserver (o creamos uno nuevo).
Dentro, cambiamos la línea de listen 80 a listen 8080.

![Descripción de la imagen](images/41.png)

En el servidor web, cambiamos el puerto de escucha en Nginx.
En vez del puerto 80, lo configuramos para que escuche en el puerto 8080.

![Descripción de la imagen](images/42.png)

Luego, eliminamos el enlace simbólico actual en /etc/nginx/sites-enabled/ y creamos uno nuevo apuntando al archivo que acabamos de modificar.

![Descripción de la imagen](images/43.png)

Finalmente, reiniciamos Nginx para aplicar los cambios con sudo systemctl restart nginx

![Descripción de la imagen](images/44.png)

## Configurar el proxy inverso
Primero debemos modificar el arhivo de configuracion de la maquina servidorweb en el archivo host de la maquina proxy. 

![Descripción de la imagen](images/50.png)

En la máquina que funcionará como proxy inverso, creamos un archivo de configuración en /etc/nginx/sites-available/ejemplo-proxy.

![Descripción de la imagen](images/45.png)

Aquí, añadimos una directiva proxy_pass que redirija las solicitudes al servidor web, usando su dirección IP y el puerto 8080 que configuramos antes.
Esto hará que cualquier solicitud que llegue al proxy en el puerto 80 sea redirigida a nuestro servidor web.

![Descripción de la imagen](images/46.png)

Habilitamos el sitio creando un enlace simbólico en /etc/nginx/sites-enabled/ejemplo-proxy y Reiniciamos el servicio Nginx.

![Descripción de la imagen](images/47.png)

A continuación se procederá a modificar el archivo hosts de la maquina anfitriona para que la ip coincida con la de la maquina de webserver

![Descripción de la imagen](images/52.png)

## Realizar pruebas
Para comprobar que todo funciona, abrimos el navegador e ingresamos la IP del proxy (o el nombre de dominio, si lo tenemos configurado).
Las solicitudes que llegan al proxy deben ser redirigidas automáticamente al servidor web.

![Descripción de la imagen](images/51.png)

Si todo está bien configurado, al hacer la solicitud deberíamos ver el contenido servido desde el servidor web

## Cabeceras

Para añadir cabeceras, en el archivo de configuración del sitio web debemos añadir dentro del bloque location / { … } debemos añadir lo siguiente:
- add_header Host nombre_del_host;

![Descripción de la imagen](images/53.png)

Aquí se muestra el resultado final

![Descripción de la imagen](images/54e.png)

![Descripción de la imagen](images/55.png)