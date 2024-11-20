# **Práctica 3.2: Despliegue de aplicaciones con Node Express**

## Introducción

En esta práctica despleguaremos aplicaciones con Node Express.

Lo pimero será parar el servicio de Tomcat para evitar problemas cuando despleguemos la aplicación.

![Descripción de la imagen](images/101.png)

## Instalación de Node.js, Express y test de la primera aplicación

Instalamos node.js y nmp con un solo comando

![Descripción de la imagen](images/102.png)

Comprobamos que la instalación se ha realizado correctamente

![Descripción de la imagen](images/103.png)

## Despliegue de una Nueva Aplicación

Clonaremos el repositorio de una aplicación de predicción meteorológica a nuestra maquina

![Descripción de la imagen](images/104.png)

instalaremos las dependencias de la aplicación dentro de la carpeta

![Descripción de la imagen](images/105.png)

En esta parte nos saldrá un error en la instalación de las dependencias, `sh: 1: nodemon: not found`. Por lo que para solucionarlo ejecutaremos este otro comando:

![Descripción de la imagen](images/106.png)

Una vez hechos los pasos si accedemos a la dirección `http://localhost:3000/`, mostrará el resultado final:

![Descripción de la imagen](images/107.png)

## Cuestiones

**¿Donde podemos ver que script se está ejecutando?**

En el archivo package.json, dentro de la sección "scripts".

**¿Qué comando está ejecutando?**

En este caso, el script start ejecuta el comando `node index.js`

Esto significa que npm run start le dice a Node.js que ejecute el archivo index.js.