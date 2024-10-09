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

## Paso 2:Creación de las carpeta del sitio web

Ahora necesitamos crear un directorio donde se alojará nuestro sitio web. Normalmente, este se encuentra en /var/www.
Usaremos mkdir para crear una nueva carpeta. 

- sudo mkdir -p /var/www/nombre_web/html

![Descripción de la imagen](images/3.png)

Ahí, dentro de esa carpeta html, debéis clonar el siguiente repositorio:

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

http://IP-maq-virtual

Lo que muestra que todo está correcto.

## Paso 3:Configuración de servidor web NGINX









