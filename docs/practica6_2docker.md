# **Práctica 6.2 - Despliegue de una aplicación PHP con Nginx y MySQL usando Docker y Docker-Compose**

## Proceso de dockerización de Nginx+PHP+MySQL

primeronos nos conectamos por ssh nuestra maquina virtual

![Descripción de la imagen](images/312.png)

### 1.Estructura de Directorios

Creamos una estructura de directorios como la siguiente:

![Descripción de la imagen](images/313.png)

![Descripción de la imagen](images/314.png)

### 2.Creación de un Contenedor Nginx

El siguiente paso será crear un contenedor Nginx para alojar la aplicacion PHP

tendremos que editar el archivo "docker-compose.yml"

![Descripción de la imagen](images/315.png)

Iniciamos el contenedor de Nginx y comprobamos que todo funciona como debe.

![Descripción de la imagen](images/316.png)

Descargará la última versión de la imagen de Nginx, creará un contenedor  y mapeará el puerto 80 del contenedor al puerto 8081 del host.

Si accedemos a la dirección localhost y su puerto 8081 mostrará lo siguiente:

![Descripción de la imagen](images/317.png)

### 3.Creación de un Contenedor PHP

Tendremos que Editar el archivo index.php de la siguiente manera:

![Descripción de la imagen](images/318.png)

el siguiente paso será crear el archivo de configuración default.conf en la carpeta nginx como en lo siguiente:

![Descripción de la imagen](images/319.png)

también se deberá modificar el archivo Dockerfile dentro del directorio nginx.

![Descripción de la imagen](images/320.png)

despues modificamos el archivo docker-compose.yml ( he modificado el puerto porque el 8081 me daba problemas )

![Descripción de la imagen](images/321.png)

Ahora levantamos los contenedores y comprobamos que todo se queda funcionando

![Descripción de la imagen](images/322.png)


Si accedemos a la dirección http://localhost:8082 deberá mostrar que funciona:

![Descripción de la imagen](images/323.png)

### 4.Creación de un Contenedor para Datos

En este apartado se debe crear un contenedor para almacenar datos, deberemos hacerlo modificando el archivo "docker-compose.yml" como se indica:

![Descripción de la imagen](images/324.png)

Comprobamos que funciona

![Descripción de la imagen](images/325.png)

![Descripción de la imagen](images/326.png)

### 5.Creación de un Contenedor MySQL

Lo siguiente será crear el contenedor MySQL para alojar la base de datos de la aplicación PHP.

Primero modificamos el archivo dockerfile del directorio php:

![Descripción de la imagen](images/327.png)

Despues modificamos el archivo docker-compose.yml añadiendo lo siguiente:

![Descripción de la imagen](images/328.png)

Tendremos que modificar el archivo index.php de la siguiente manera:

![Descripción de la imagen](images/329.png)

Ahora comprobaremos que el contenedore de MYSQL funiona correctamente

![Descripción de la imagen](images/330.png)

### 6.Verificación de Conexión a la Base de Datos

Si ahora accedemos a http://localhost:8082, deberíamos obtener la siguiente pantalla:

![Descripción de la imagen](images/331.png)

Pero si se modificamos el archivo `index.php` con el siguiente contenido:

```php	
    $user = 'root';
    $password = 'secret';
```

![Descripción de la imagen](images/332.png)

Si se accede a la dirección http://localhost:8082 (Yo lo he hecho en el puerto 8082) deberá aparecer lo siguiente:

![Descripción de la imagen](images/333.png)

Esto significa que todo el proceso se ha realizado correctamente.

### 7.Esquema de la Aplicación

![Descripción de la imagen](images/334.png) 

