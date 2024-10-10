# **Despliegue de un Sitio Web con Nginx**

## Introducción
En esta práctica, desplegamos un servidor web utilizando **Nginx** en un sistema basado en Debian/Ubuntu. 
A través de la instalación y configuración básica, conseguimos servir un sitio web estático de ejemplo. 

## Paso 1: Instalación de Nginx
Primero, actualizamos los paquetes e instalamos Nginx:

- sudo apt update
- sudo apt install nginx

![Descripción de la imagen](images/1.png)

Verificamos que Nginx esté corriendo con el siguiente comando:

- systemctl status nginx

![Descripción de la imagen](images/2.png)

Si todo está bien, debe mostrar que el servicio está activo.

## Paso 2: Creación de las carpeta del sitio web

Ahora necesitamos crear un directorio donde se alojará nuestro sitio web. Normalmente, este se encuentra en /var/www.
Usaremos mkdir para crear una nueva carpeta. 

- sudo mkdir -p /var/www/nombre_web/html

![Descripción de la imagen](images/3.png)

Ahí, dentro de esa carpeta html, debémos clonar el siguiente repositorio:

![Descripción de la imagen](images/7.png)

https://github.com/cloudacademy/static-website-example

Es importante cambiar la propiedad de este directorio a www-data, que es el usuario bajo el cual Nginx se ejecuta. Hacemos esto con:

- sudo chown -R www-data:www-data /var/www/nombre_web/html

Luego, ajustamos los permisos para que Nginx tenga acceso adecuado:

- sudo chmod -R 755 /var/www/nombre_web

![Descripción de la imagen](images/4.png)

Para comprobar que el servidor está funcionando correctamente:

miramos la ip de la maquina con el siguiente comando

- hostname -I

![Descripción de la imagen](images/5.png)

Despues buscamos en internet la ip de la maquina y debería de salir algo tal que así

![Descripción de la imagen](images/6.png)

- http://IP-maq-virtual

Lo que muestra que todo está correcto.

## Paso 3: Configuración de servidor web NGINX

El siguiente paso es crear un archivo de configuración para nuestro sitio. Nos dirigimos a la carpeta de configuración de Nginx:

- sudo nano /etc/nginx/sites-available/nombre_web

![Descripción de la imagen](images/9.png)

Para encontrar la ruta deberemos usar el siguiente comando:

![Descripción de la imagen](images/10.png)

- sudo find / -name index.html

Dentro de este archivo, añadimos lo siguiente:

![Descripción de la imagen](images/8.png)

Después de guardar el archivo, necesitamos habilitar este nuevo sitio creando un enlace simbólico en la carpeta sites-enabled:

![Descripción de la imagen](images/11.png)

- sudo ln -s /etc/nginx/sites-available/mi_sitio /etc/nginx/sites-enabled/

Para que los cambios surtan efecto, reiniciamos Nginx con:

![Descripción de la imagen](images/12.png)

- sudo systemctl restart nginx

## Paso 4: Comprobaciones

Primero añadimos la ip de la maquina virtual en la siguiente ruta

- en Linux: /etc/hosts

![Descripción de la imagen](images/13.png)

El siguiente paso será añadir la ip nuestro pc en la que estamos usando la maquina para poder conectarnos posteriormente

- en Windows: C:\Windows\System32\drivers\etc\hosts


![Descripción de la imagen](images/14x.png)

![Descripción de la imagen](images/15.png)

![Descripción de la imagen](images/16.png)

![Descripción de la imagen](images/17.png)

![Descripción de la imagen](images/18.png)

![Descripción de la imagen](images/19.png)

![Descripción de la imagen](images/20.png)

![Descripción de la imagen](images/21.png)

![Descripción de la imagen](images/22.png)











