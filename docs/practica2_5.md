# **Práctica 2.4 - Proxy inverso y balanceo de carga con SSL en NGINX**

### Creación de certificado autofirmado

Para esta practica vamos a necesitar un certificado SSL autofirmado

Primero, dentro del directorio de NGINX (/etc/nginx/), creamos una carpeta llamada ssl para guardar los archivos SSL.
Luego, con el comando openssl, generamos un certificado y una clave privada.
Esto es un certificado “autofirmado”, o sea, no es de una entidad oficial. Lo usamos solo para pruebas.

![Descripción de la imagen](images/73.png)
![Descripción de la imagen](images/74.png)

### Configuración SSL en el proxy inverso

En el archivo /etc/nginx/sites-available/balanceo, agregamos la configuración para que NGINX escuche en el puerto 443 (para HTTPS).
Añadimos las rutas al certificado y la clave privada, y definimos los protocolos y cifrados de SSL que permitimos.Esto asegura que el tráfico esté cifrado.

![Descripción de la imagen](images/75.png)

reiniciamos el servidor para aplicar los cambios

![Descripción de la imagen](images/76.png)

### Comprobaciones
Probamos accediendo al sitio en HTTPS. Veremos una advertencia del navegador sobre el certificado autofirmado, pero es normal.

![Descripción de la imagen](images/77.png)

![Descripción de la imagen](images/78.png)

![Descripción de la imagen](images/79.png)
