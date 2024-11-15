# **Práctica 3.1: Instalación de Tomcat y Maven para despliegue de aplicación Java**
## Instalación y Despliegue Tomcat
Lo primero que haremos será Descargar Apache Tomcat 10 y extraerlo en nuestra máquina. 
Podemos configurarlo para que funcione en el puerto 8080 (predeterminado).
Descargamos el JDK con el siguiente comando

![Descripción de la imagen](images/82.png)

comprobaremos la versión instalada 

![Descripción de la imagen](images/83.png)

Seguiremos con la instalación de Tomcat con el siguiente comando

![Descripción de la imagen](images/84.png)

El siguiente paso será configurar el archivo tomcat-users.xml en la carpeta de Tomcat para crear un usuario con roles de administrador (manager-gui) y de despliegue (manager-script).

- sudo nano /etc/tomcat10/tomcat-users.xml

![Descripción de la imagen](images/85.png)

Hecho este paso pasaremos a reiniar el servicio de Tomcat con el comando `sudo systemctl restart tomcat`. Para comprobar que el servicio se ha iniciado correctamente, se ejecutará el comando `sudo systemctl status tomcat` y debera aparecer algo similar a lo siguiente:
Que como se puede comprobar el servicio de tomcat esta activo y correcto.

![Descripción de la imagen](images/86.png)

Cambie mi nombre a "manager" porque me daba errores.

Accedemos a la dirección `http://localhost:8080/nombre_usuario/html` nos solicitará usuario y contraseña y nos mostrará lo siguiente:

![Descripción de la imagen](images/87.png)

![Descripción de la imagen](images/88.png)

Ahora pasaremos a desplegar un un archivo .war en Tomcat.
El archivo .war de la entrega cotiene errores, por lo que elegiré un archivo .war con un proyecto de ejemplo.

Desde el siguiente enlace se descargará el proyecto de ejemplo: `https://tomcat.apache.org/tomcat-6.0-doc/appdev/sample/`


Selecionamos el archivo war y le damos a desplegar

![Descripción de la imagen](images/89.png)

Nos mostrará el archivo desplegado

![Descripción de la imagen](images/90.png)

podremos acceder al archivo

![Descripción de la imagen](images/91.png)

## Instalación y Despliegue Maven

El primer paso será instalar maven

![Descripción de la imagen](images/92.png)
![Descripción de la imagen](images/93.png)

Añadiermos un nuevo usuario para maven en el archivo `tomcat-users.xml` para poder usarlo a la hora de desplegar maven

![Descripción de la imagen](images/94.png)

lo siguiente será configurar Maven, modificaremos el archivo `settings.xml` y Debería quedar tal que así:

![Descripción de la imagen](images/95.png)

Y se clona el repositorio de ejemplo facilitado para desplegarlo con Maven.

![Descripción de la imagen](images/96.png)

Por ultimo se editará el archivo `pom.xml` y la configuración. Como se muestra:

![Descripción de la imagen](images/97.png)

Si todo está correcto y ejecutamos el comando `mvn tomcat7:deploy` deberá aparecer algo así:

![Descripción de la imagen](images/98.png)

Si accedemos a la dirección `http://localhost:8080/nombre_usuario/` nos mostrará correctamente

![Descripción de la imagen](images/99.png)

podremos acceder al archivo final.

![Descripción de la imagen](images/100.png)

## Cuestiones

*Solución:*

Esto se debe a la facilidad de configuración y a la presunción de que Tomcat se empleará en entornos seguros y bien gestionados. Sin embargo, en entornos de producción, se aconseja evitar esta práctica mediante el uso de autenticación externa.


