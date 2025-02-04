# **ejercicios Git y GitHub**

## Repositorio DEAW

Empezaremos Creando un repositorio en nuestro GitHub llamado DEAW.

![Descripción de la imagen](images/234.png)

Clonamos el repositorio en local.

![Descripción de la imagen](images/235.png)

## Readme.md
dentro de nuestro repositorio local crearemos un documento README.md

![Descripción de la imagen](images/236.png)

![Descripción de la imagen](images/237.png)

## Commit
haremos el primer commit con el comentario

![Descripción de la imagen](images/238.png)

## Push

Subiremos los cambios al repositorio de la siguiente manera

![Descripción de la imagen](images/239.png)

para comprobarlo veremos el .md en el repositorio

![Descripción de la imagen](images/240.png)

## Ignorar archivos

A veces, hay archivos o carpetas que no queremos incluir en el repositorio, ya sea porque contienen información sensible (contraseñas, claves API), archivos temporales, o simplemente porque no son necesarios en GitHub.

Para ello, usamos un archivo especial llamado .gitignore, que le dice a Git qué archivos y carpetas debe ignorar.

Creamos en el repositorio local un fichero llamado privado.txt.

Creamos en el repositorio local una carpeta llamada privada.

Realizamos los cambios oportunos para que tanto el archivo como la carpeta sean ignorados por git.

![Descripción de la imagen](images/241.png)

![Descripción de la imagen](images/242.png)

![Descripción de la imagen](images/243.png)

## Añadir fichero 1.txt

![Descripción de la imagen](images/244.png)

Al hacer esto, se deberá hacer un push, para que lo muestre en el repositorio.

![Descripción de la imagen](images/245.png)

## Crear un tag y subirlo al repositorio remoto

Los tags en Git se usan para marcar versiones importantes del código, como hitos o lanzamientos de software.

![Descripción de la imagen](images/246.png)

En este caso, hemos creado el tag v0.1 para marcar la primera versión del repositorio.

![Descripción de la imagen](images/247.png)

## Cuenta de GitHub

Poner una foto en vuestro perfil de GitHub.

![Descripción de la imagen](images/248.png)

Poner el doble factor de autentificación en vuestra cuenta de GitHub.

La autenticación en dos factores (2FA) mejora la seguridad de tu cuenta, ya que además de tu contraseña, necesitarás un código adicional para iniciar sesión.

📌 Paso 1: Acceder a la configuración de seguridad
1️⃣ Inicia sesión en GitHub: https://github.com/
2️⃣ Ve a la esquina superior derecha y haz clic en tu foto de perfil.
3️⃣ Selecciona "Settings" (Configuración).
4️⃣ En el menú izquierdo, haz clic en "Password and authentication" (Contraseña y autenticación).

![Descripción de la imagen](images/249.png)

## Uso Social de Github

Preguntar los nombres de usuario de GitHub de 2 de tus compañeros de clase, búscalos, y sigueles.

![Descripción de la imagen](images/250.png)

Seguir los repositorios DEAW del resto de tus compañeros.

Añadir una estrella a los repositorios DEAW del resto de tus compañeros.

![Descripción de la imagen](images/251.png)

## Crear una tabla

Crear una tabla en el fichero README.md con la información básica de los compañeros de clase.

![Descripción de la imagen](images/252.png)

![Descripción de la imagen](images/253.png)

## Colaboradores

Añadiremos a un compañero de clase como colaborador del repositorio DEAW.

![Descripción de la imagen](images/254.png)

## Crear una rama v0.2 y añadir un fichero 2.txt

Crearemos una rama v0.2 y cambiamos a esa rama.

![Descripción de la imagen](images/255.png)

![Descripción de la imagen](images/256.png)

## Merge Directo

Haremos un merge de la rama v0.2 en la rama master.

![Descripción de la imagen](images/257.png)

## Merge con conflicto

En la rama master poner Hola en el fichero 1.txt y hacer commit.

Posicionarse en la rama v0.2 y poner Adios en el fichero "1.txt" y hacer commit.

Posicionarse de nuevo en la rama master y hacer un merge con la rama v0.2

![Descripción de la imagen](images/258.png)

![Descripción de la imagen](images/259.png)

Debemos elegir una versión o combinarlas. por ejemplo podemos cambiar a Hola y adiós.

![Descripción de la imagen](images/260.png)

## Listado de ramas

![Descripción de la imagen](images/261.png)

en mi caso, después de hacer el merge, todo se ha fusionado correctamente, y por eso git branch --no-merged no muestra ninguna rama.

Cuando se realiza un merge correcto de la rama v0.2 en main, esa rama ya no aparece como no fusionada

Es normal que v0.2 no aparezca en git branch --no-merged si ya está fusionada.

![Descripción de la imagen](images/262.png)







