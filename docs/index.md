# **Práctica 2.1 - Despliegue de un Sitio Web con Nginx**

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

Ahora pasaremos a la configuración del servidor SFTPD.
En primer lugar, lo instalaremos desde los repositorios:

- sudo apt-get update
- sudo apt-get install vsftpd

El comando sudo apt-get install vsftpd instala el paquete vsftpd, que es un servidor FTP ligero y seguro. 

Despues creamos una carpeta en nuestro home en Debian:
- mkdir /home/mario_web/ftp

![Descripción de la imagen](images/15.png)

En la configuración de vsftpd indicaremos que este será el directorio al cual vsftpd se cambia después de conectarse el usuario.

El siguiente paso será crear los certificados de seguridad necesarios para aportar la capa de cifrado a nuestra conexión.


![Descripción de la imagen](images/16.png)

Usaremos el siguiente comando para la configuración de vsftpd.

- sudo nano /etc/vsftpd.conf

![Descripción de la imagen](images/16.png)

Dentro de la configuración de vsftpd añadiremos lo siguiente que se muestra en la imagen.
Esta configuración asegura que las conexiones FTP sean seguras usando FTPS (FTP sobre SSL/TLS).
Esto cifra tanto la autenticación como la transferencia de archivos, protegiendo los datos de posibles intercepciones.

![Descripción de la imagen](images/17.png)

Ya hemos terminado con la configuración. 
Ahora podremos acceder a nuestro servidor mediante un cliente FTP descargando filezilla client en el cliente

![Descripción de la imagen](images/18.png)
Entramos en filezilla e introducimos los datos necesarios para conectarnos a nuestro servidor FTP en Debian

- IP de la maquina servidor
- Nombre
- Contraseña
- Puerto, que será el 21

Como muestro en la imagen ya conectado a la maquina principal he pasado un archivo txt para combrobar que funciona correctamente.

![Descripción de la imagen](images/19.png)

Por ultimo modificaremos la configuración del servidor web con Nginx, para poder mostrar la pagina final.

Este archivo configura mi servidor web que sirve contenido estático desde /var/www/mario_web y asegura la conexión usando HTTPS.
El puerto 80 redirige automáticamente al 443 (HTTPS) para garantizar conexiones seguras.

![Descripción de la imagen](images/20.png)

Para comprobar que la configuración está correctamente y nos muestra la página,
escribiremos en internet "https://www.mario_web.com/""

Nos saldra un mensaje de advertencia, para poder visualizar la pagina pincharemos en "configuración avanzada" y despues en "Acceder a www.mario_web.com (sitio no seguro)""

![Descripción de la imagen](images/21.png)

Finalmente visualizará la pagina final mostrando que todo el proceso realizado está correcto

![Descripción de la imagen](images/22.png)

# **Práctica 2.2 - Autenticación en Nginx**

## Introducción
La práctica 2.2 trata sobre cómo configurar autenticación básica en un servidor Nginx.
El objetivo es proteger el acceso a ciertos recursos web usando usuarios y contraseñas.
Se trabaja con la creación del archivo .htpasswd para almacenar credenciales cifradas, se configuran las directivas de autenticación en Nginx,
y se realizan pruebas para asegurar que la autenticación funcione. 
También se explora cómo combinar autenticación con restricciones por IP. 
La práctica incluye tareas como modificar la configuración y analizar los logs de acceso.

Paquetes necesarios:

En primer lugar debemos comprobar si el paquete está instalado con el siguiente comando:

- dpkg -l | grep openssl

![Descripción de la imagen](images/24.png)

Y si no lo estuviera, instalarlo.

### Creación de usuarios y contraseñas para el acceso web

Crearemos un archivo oculto llamado “.htpasswd” en el directorio de configuración /etc/nginx donde guardar nuestros usuarios y contraseñas:

![Descripción de la imagen](images/25.png)

Ahora crearemos un pasword cifrado para el usuario:

Nos pedirá la contraseña que queramos y verificarla.

![Descripción de la imagen](images/26.png)

Crearemos otro usuario con mis apellidos y con el siguiente comando se mostrarán las contraseñas cifradas

- cat /etc/nginx/.htpasswd

![Descripción de la imagen](images/27.png)

### COMPROBACIÓN 1

Al entrar en nuestra web nos pedirá el usuario y contraseña.

![Descripción de la imagen](images/28.png)

### COMPROBACIÓN 2

En caso de no poder acceder mostrará los siguiente

![Descripción de la imagen](images/29.png)

### TAREA 1

Aquí se muestra 3 intentos fallidos de autenticación usando el siguiente comando:

- sudo nano /var/log/nginx/error.log

![Descripción de la imagen](images/30.png)

### TAREA 2
Borramos las dos líneas que hacen referencia a la autenticación básica en el location del directorio raíz.

![Descripción de la imagen](images/32.png)

Despues, añadimos un nuevo location debajo con la autenticación básica para el archivo/sección contact.html únicamente.

![Descripción de la imagen](images/31.png)

Al haber hecho esto solo podremos acceder al apartado de "contact"

![Descripción de la imagen](images/33.png)

### Combinación de la autenticación básica con la restricción de acceso por IP

### Tarea 1

Entraremos en el archivo de configuración y añadiremos el deny junto a la dirección IP 

![Descripción de la imagen](images/34.png)

Cuando configuramos Nginx con autenticación básica, cualquier intento fallido de acceder con credenciales incorrectas se registra en los logs. En este caso, primero intentaremos acceder con un usuario no válido y luego con uno correcto.

Nos mostrará el siguiente error:

![Descripción de la imagen](images/35.png)

Para ver los usuarios que han accedido correctamente a la pagina sería usando el siguiente comando:

- sudo cat /var/log/nginx/access.log

![Descripción de la imagen](images/38.png)

### Tarea 2

Para esta tarea haremos lo mismo pero añadiendo lo siguiente:


![Descripción de la imagen](images/36.png)

Ahora si nos dejará acceder a la página ya que no se deniega la ip.

![Descripción de la imagen](images/37.png)

### Cuestiones Finales

### Cuestion 1

Si yo tengo la IP 172.1.10.15 y estoy intentando acceder al directorio /web_muy_guay con un usuario y contraseña incorrectos, no podré acceder. Esto se debe a que en la configuración del bloque location se usa la directiva satisfy all, lo que significa que tanto la autenticación básica como la restricción por IP deben cumplirse. Aunque mi IP está permitida (allow 172.1.10.15), al equivocarme con las credenciales, no cumplo con la autenticación básica, y por lo tanto el acceso será denegado.

### Cuestion 2
Si ahora intento acceder al directorio /web_muy_guay con mi IP (172.1.10.15) e ingreso correctamente el usuario y contraseña, sí podré acceder. En este caso, la directiva sigue siendo satisfy all, por lo que ambas condiciones (IP permitida y autenticación exitosa) deben cumplirse. Mi IP está permitida y al haber introducido correctamente las credenciales, cumplo con los dos requisitos, por lo que podré entrar sin problemas.

### Cuestion 3

En este caso, aunque introduzca correctamente el usuario y la contraseña, no podré acceder. La razón es que la directiva satisfy any permite que se cumpla solo una de las condiciones (autenticación o IP permitida) para permitir el acceso. Sin embargo, en la configuración se ha añadido una regla que deniega el acceso a mi IP (deny 172.1.10.15), lo que bloquea mi acceso incluso si la autenticación es exitosa. La regla de denegación de la IP tiene prioridad en este caso, así que el acceso es bloqueado.

### Cuestion 4

Para proteger el directorio /Proyectos de mi web, lo que haría sería añadir un bloque location específico para ese directorio, con autenticación básica. La configuración quedaría algo así:

nginx
server {
    listen 80;
    listen [::]:80;
    root /var/www/freewebsitetemplates.com/preview/space-science;
    index index.html index.htm index.nginx-debian.html;
    server_name freewebsitetemplates.com www.freewebsitetemplates.com;

    location / {
        try_files $uri $uri/ =404;
    }

    location /Proyectos {
        auth_basic "Área restringida - Proyectos";
        auth_basic_user_file /etc/nginx/conf.d/htpasswd_proyectos;
    }
}

Aquí lo que hago es configurar el acceso restringido para el directorio /Proyectos usando la autenticación básica con un archivo de contraseñas (htpasswd). De esta forma, solo quienes tengan el usuario y la contraseña correcta podrán acceder al directorio.

# **Práctica 2.1 - Despliegue de un Sitio Web con Nginx**


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

# **Práctica 2.1 - Balanceo de carga con proxy inverso en Nginx**

## Introducción

Esta práctica introduce el concepto de balanceo de carga mediante un proxy inverso con Nginx.
Aquí veremos cómo distribuir tráfico entre varios servidores, lo que mejora la disponibilidad y eficiencia del servicio web.
El objetivo es configurar un proxy inverso que reparta las solicitudes entre dos servidores diferentes, de manera que se garantice el acceso incluso si uno de ellos falla.
Además, se explorarán varios métodos de balanceo para entender cuál es más efectivo en distintas situaciones.

##CONFIGURACIÓN DE LOS SERVIDORES WEB

- Webserver1:

Desactivamos los sitios web de las practicas anteriores

![Descripción de la imagen](images/58.png)

Lo Primero que haremos será cambiarle el nombre al archivo de conf

![Descripción de la imagen](images/56.png)

Despues le quitaremos el link simbolico anterior lo volvemos a crear y reiniciamos el servicio de nginx.

![Descripción de la imagen](images/56.png)

Creamos el archivo de configuracion para webserver1 en la carpeta /etc/nginx/sites-available y enlazamos a sites-enabled
```
server {
    listen 8080;
    server_name webserver1;

    root /var/www/webserver1/html;
    index index.html;

    add_header Serv_Web1 "tu_nombre";

    location / {
        try_files $uri $uri/ =404;
    }
}
```
Después de poner esto en el archivo /etc/nginx/sites-available/webserver1 enlazamos a sites-enables con el siguiente comando.

![Descripción de la imagen](images/59.png)

![Descripción de la imagen](images/60.png)

Lo siguiente será Crear el directorio /var/www/webserver1/html y creamos en él, el archivo index.html

```html
<html lang="es">
<head>
    <title>Prueba de balanceo de carga con Nginx</title>
</head>
<body>
    <h2>Este es el servidor web 1</h2>
    <p>Comprueba el balanceo de carga con Nginx recargando esta página</p>>
</body>
</html>
```
![Descripción de la imagen](images/62.png)

reiniciamos y comprobamos el servidor nginx

![Descripción de la imagen](images/63.png)

Una vez hecho todo esto podemos pasar a clonar la maquina virtual.

- Webserver2:
Aqúi solamente habrá que repetir el proceso que ya hemos hecho pero cambiando webserver1 por Webserver2.

Modificamos configuración

![Descripción de la imagen](images/64.png)

modificamos index.html

![Descripción de la imagen](images/65.png)

por ultimo reiniciamos y comprobamos el servidor nginx

![Descripción de la imagen](images/66.png)

##CONFIGURACIÓN DEL PROXY INVERSO

Entramos en la máquina que configuramos el proxy inverso en la práctica anterior







Realizado por Mario Jurado Ayuso
























