# **Práctica 3.5 - Despliegue de una aplicación Flask**

Para poder realizar esta practica necesitaremos tener previamente estos paquetes instalados: `Nginx`, `Gunicorn` y `Pipenv`.

## Procedimiento completo para el despliegue

El primer paso será Actualizar los repositorios de paquetes del sistema e Instalar Python.

![Descripción de la imagen](images/152.png)

Además instalaremos el paquete pipenv que se encargará de gestionar los entornos virtuales y comprobamos su versión

![Descripción de la imagen](images/153.png)

![Descripción de la imagen](images/154.png)

Creamos el directorio en el que almacenaremos nuestro proyecto:

![Descripción de la imagen](images/155.png)

Como lo creamos con `sudo`, los permisos pertenecen al usuario root del sistema:

![Descripción de la imagen](images/156.png)

Hay que cambiar los permisos para que pertenezcan a nuestro usuario y pertenezca al grupo www-data.

![Descripción de la imagen](images/157.png)

Tendremos que Establecer los permisos adecuados para que pueda ser leído por todo el mundo

![Descripción de la imagen](images/158.png)

dentro del directorio creado se creará el archivo oculto `.env`

![Descripción de la imagen](images/159.png)

que contendrá las variables de entorno con el comando

![Descripción de la imagen](images/160.png)

verificamos los cambios con `cat .env`

![Descripción de la imagen](images/161.png)

Iniciaremos el entorno virtual y Pipenv cargará las dependencias del archivo .env

![Descripción de la imagen](images/162.png)

Lo siguiente será instalar las dependencias necesarias para nuestro proyecto

![Descripción de la imagen](images/163.png)

Se crearán los archivos `app.py` y `wsgi.py`  que contendrán lo siguiente:

![Descripción de la imagen](images/164.png)

ahora ejecutaremos nuestra aplicación a modo de comprobación con el servidor web integrado de Flask

especificamos la dirección 0.0.0.0 para que escuche en todas sus interfaces.

![Descripción de la imagen](images/165.png)

Ahora accedemos desde nuestro navegador a la dirección proporcionada `http://IP-maq-virtual:5000` y nos debería mostrar ver lo siguiente:

![Descripción de la imagen](images/166.png)

comprobaremos que Gunicorn funciona correctamente:

![Descripción de la imagen](images/167.png)

debemos tomar nota de cual es el path o ruta desde la que se ejecuta gunicorn para poder configurar más adelante un servicio del sistema. 

Con el siguiente comando:

![Descripción de la imagen](images/168.png)

Por último, salimos del entorno virtual con `deactivate`

![Descripción de la imagen](images/169.png)

El siguiente paso será Iniciar Nginx y comprobar que su estado sea activo.

![Descripción de la imagen](images/170.png)

Se creará un archivo de configuración para que systemd ejecute Gunicorn como otro servicio mas:

![Descripción de la imagen](images/171.png)

habilitamos el servicio lo iniciamos y comprobamos que está en funcionamiento:

![Descripción de la imagen](images/172.png)

Ahora crearemos un archivo de configuración en Nginx y lo configuraremos de la siguiente manera.

![Descripción de la imagen](images/173.png)

despues crearemos el enlace simbólico para que Nginx pueda acceder a los archivos de la aplicación:

![Descripción de la imagen](images/174.png)

Comprobaremos que la configuración de Nginx es correcta:

![Descripción de la imagen](images/175.png)

editamos el archivo /etc/hosts de nuestra máquina para que asocie la IP de la máquina virtual:

![Descripción de la imagen](images/176.png)

Por ultimo accedemos a nuestro navegador para comprobar que funciona.

![Descripción de la imagen](images/177.png)

## Ejercicio

Repetimos todo el proceso con la aplicación del siguiente repositorio: https://github.com/raul-profesor/Practica-3.5.








