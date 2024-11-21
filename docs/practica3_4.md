# **Práctica 3.4: Despliegue de una Aplicación React en Netlify (PaaS)**

## Creación de nuestra aplicación

Para realizar la practica nos conectaremos por ssh a nuestra maquina.

![Descripción de la imagen](images/108.png)

Lo primero será crear una carpeta en el escritorio y dentro de esta, tres archivos: `head.html`, `tail.html` y `aplicacion.js`.

![Descripción de la imagen](images/109.png)

El archivo `head.html` contendrá lo siguiente:

![Descripción de la imagen](images/110.png)

El archivo `tail.html` contendrá lo siguiente:

![Descripción de la imagen](images/111.png)

El archivo `aplicacion.js` contendrá lo siguiente:

![Descripción de la imagen](images/112.png)

Para inicializar el proyeto usaremos `npm init` nos pedirá algunos datos a rellenar. 

Despues ejecutaremos la aplicación usando `node aplicacion.js`.

![Descripción de la imagen](images/113.png)

Si accedemos a la dirección `http://localhost:8080/` desde nuestra maquina nos mostrará lo siguiente:

![Descripción de la imagen](images/114.png)

## Aplicación para Netlify

Para desplegar nuestra aplicación en Netlify, vamos a clonar el repositorio para esta practica

![Descripción de la imagen](images/115.png)

## Proceso de Despliegue en Netlify

Se va a desplegar en netlify de dos maneras diferentes.

- Despliegue manual desde el CLI de Netlify, es decir, desde el terminal, a partir de un directorio local de nuestra máquina.

- Despliegue desde un código publicado en uno de nuestros repositorios de Github

### Despliegue Mediante CLI
En este metodo instalaremos el cliente de Netlify dentro de la carpeta de la aplicación.

![Descripción de la imagen](images/116.png)

Para poder loguearnos debemos entrar en netlify, autenticarnos, aceptar la solicitud y crear un token:

![Descripción de la imagen](images/118.png)

![Descripción de la imagen](images/119.png)

![Descripción de la imagen](images/120.png)

![Descripción de la imagen](images/121.png)

una vez ya hecho el siguiente paso será loggearnos en la cuenta de Netlify.

![Descripción de la imagen](images/117.png)

Ahora instalaremos npm en la aplicación y ya podremos desplegar la aplicación en Netlify

![Descripción de la imagen](images/122.png)

![Descripción de la imagen](images/123.png)

El siguiente paso será desplegar netlify, Se creará y configurará un nuevo sitio

![Descripción de la imagen](images/124.png)

![Descripción de la imagen](images/125.png)

Para comprobar que se ha creado correctamente entraremos en la url de la pagina que nos proporciona netlify.

![Descripción de la imagen](images/126.png)

![Descripción de la imagen](images/127.png)

## Despliegue mediante conexión con Github

En primer lugar, vamos a eliminar el site que hemos desplegado antes en Netlify para evitarnos cualquier problema y/o conflicto:

![Descripción de la imagen](images/128.png)

Tambien tendremos que borrar el directorio que clonamos anteriormente con este comando `rm -rf color-shades-generator`. 

![Descripción de la imagen](images/129.png)

nos descargaremos los fuentes en formato .zip

![Descripción de la imagen](images/130.png)

Creamos una carpeta nueva y descomprimimos dentro el zip:

![Descripción de la imagen](images/131.png)

Ahora crearemos un repositorio en github y subiremos los archivos de la practica.

![Descripción de la imagen](images/132.png)

añadiremos el contenido de la carpeta al repositorio.

![Descripción de la imagen](images/133.png)

![Descripción de la imagen](images/134.png)

Una vez hecho esto el repositorio deberia quedar tal que así:

![Descripción de la imagen](images/135.png)

El siguiente paso será enlazar nuestra cuenta de GitHub en Netlify.

![Descripción de la imagen](images/136.png)

despues selecionamos el repositorio de la practica para desplegarlo

![Descripción de la imagen](images/137.png)

Selecionamos en "Deploy"

![Descripción de la imagen](images/138.png)

Y ya tendríamos nuestra pagina desplegada correctamente como se muestra:

![Descripción de la imagen](images/139.png)

![Descripción de la imagen](images/140.png)

![Descripción de la imagen](images/141.png)

Ahora accederemos a la carpeta public y se modificará el archivo robot.txt, pondremos el nombre en disallow, y se subirá al repositorio con su commit.

![Descripción de la imagen](images/142.png)

![Descripción de la imagen](images/143.png)

![Descripción de la imagen](images/144.png)

Como podemos ver se muestra en la web: 

![Descripción de la imagen](images/145.png)

## Despliegue con Vercel

para vercel deberemos seguir los mismos pasos como anteriormente.

Enlazamos github con vercel y desplegamos la practica

![Descripción de la imagen](images/146.png)


![Descripción de la imagen](images/147.png)

Al pinchar en "deploy" nos desplegara el sitio automaticamente como se muestra:

![Descripción de la imagen](images/148.png)

![Descripción de la imagen](images/149.png)

![Descripción de la imagen](images/150.png)

Por último volvemos a modificar robot.txt

![Descripción de la imagen](images/151.png)

Este sería el ultimo paso de la practica correctamente.








