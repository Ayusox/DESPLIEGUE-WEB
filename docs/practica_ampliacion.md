# **Configuración de un Servidor Nginx con Hosts Virtuales y Directorios de Usuario**

## Conexión SSH

El pirmer paso será conectar nuestra maquina física con nuestra maquina virtual mediante ssh.

![Descripción de la imagen](images/196.png)

## Creacion de Usuarios

En este paso, creamos los usuarios necesarios utilizando el comando useradd. Es importante asignarles contraseñas seguras para garantizar la seguridad del sistema. Adicionalmente, se configuran sus directorios personales de manera automática al crearlos.

![Descripción de la imagen](images/197.png)

## Creación de las Carpetas

Una vez creados los usuarios, accedemos con cada uno de ellos mediante el comando su. En sus directorios personales, creamos la carpeta public_html utilizando mkdir. Esta carpeta será el lugar donde cada usuario almacenará los archivos de su página web.

![Descripción de la imagen](images/198.png)

## Asignar Permisos

Es esencial ajustar los permisos de las carpetas public_html para que Nginx pueda acceder al contenido sin comprometer los privilegios de los usuarios. Configuramos los permisos para que el servidor pueda leer y servir los archivos web correctamente, pero manteniendo la propiedad de los archivos en manos de cada usuario.

![Descripción de la imagen](images/200.png)

![Descripción de la imagen](images/201.png)

## Páginas Web Correspondientes

Para comprobar que todo funciona crearemos dos archivos index.html para cada usuario en las carpetas public_html.

![Descripción de la imagen](images/202.png)

![Descripción de la imagen](images/203.png)

## Configuración de Nginx

Instalaremos nginx y comprobaremos que su funcionamiento es correcto con el siguiente comando.

![Descripción de la imagen](images/204.png)

![Descripción de la imagen](images/205.png)

hasta aquí bien es siguiente pasó será generar los certificados SSL con el siguiente comando

![Descripción de la imagen](images/206.png)

![Descripción de la imagen](images/207.png)

## Configuración Hosts Virtuales

Ahora tendremos que configurar los host virtuales pero antes debemos crear el archivo en la carpeta `/etc/nginx/sites-available` en cada usuario correspondiente.

![Descripción de la imagen](images/208.png)

![Descripción de la imagen](images/209.png)

Una vez que escribímos el archivo de configuración en sites-available, no basta con que esté ahí; también hay que activarlo. Para hacerlo, en vez de copiar el archivo a /etc/nginx/sites-enabled/ (donde Nginx lee los sitios activos), crearemos un enlace simbólico para cada uno. Esto permite gestionar los sitios fácilmente, ya que podemos activarlos o desactivarlos sin mover ni duplicar archivos.

![Descripción de la imagen](images/210.png)
![Descripción de la imagen](images/211.png)

## Hosts Virtuales

El archivo hosts en C:\Windows\System32\drivers\etc\hosts permitiremos asociar manualmente direcciones IP con nombres de dominio en nuestra máquina. Para comprobar y configurar los hosts virtuales que hemos creado, debemos añadir una línea para cada host virtual que apunte a la dirección IP correspondiente.

![Descripción de la imagen](images/212.png)

No mostrará una advertencia, deberemos pulsar en "aceptar el riesgo y continuar"


![Descripción de la imagen](images/215.png)

Podremos pinchar en "ver certificado" para ver que su creación ha sido exitosa y correcta.

![Descripción de la imagen](images/213.png)
![Descripción de la imagen](images/214.png)

Finalente nos mostrará las 2 páginas de cada uno que hemos creado.