# Ejecución de PHP desde un contenedor de Docker 📦

¿Problemas a la hora de ejecutar PHP en un ordenador no compatible con 64 bits? Si eres de los que tienen que rebuscar una versión de XAMPP acorde a su sistema operativo para poder ejecutar aplicaciones PHP, **Docker** es tu solución.

Usando un contenedor con PHP/APACHE en su interior no tendrás que preocuparte de en qué máquina ejecutas tu código, será tan sencillo como alojarlo en el interior del contenedor y... ¡voila!

## Tabla de contenidos 📋

1. [Instalación de Docker Desktop](#1-Instalación-de-Docker-Desktop)
2. [Creación del archivo Dockerfile](#2-Creación-del-archivo-Dockerfile)
3. [Ejecutar el contenedor](#3-Ejecutar-el-contenedor)
4. [Ejecución de la imágen creada](#4-Ejecución-de-la-imágen-creada)
5. [Parar el contenedor](#5-Parar-el-contenedor)
6. [Limpiar contenedores](#6-Limpiar-contenedores)
7. [Uso de volúmenes](#7-Uso-de-volúmenes)
8. [Eliminar imágenes](#8-Eliminar-imágenes)
9. [Uso de versiones y más](#9-Uso-de-versiones-y-más)
10. [Documentación oficial Docher PHP](#10-Documentación-oficial-Docker-PHP-y-tutoriales)

### 1. Instalación de Docker Desktop

Previo al tutorial es necesario instalar [Docker Desktop](https://www.docker.com/products/docker-desktop).

### 2. Creación del archivo Dockerfile

Crearemos un nuevo archivo llamado **Dockerfile** en el directorio del proyecto donde colocaremos:

```
FROM php:7.4-apache
COPY: /src /var/www/html
EXPOSE 80
```
* **FROM php:7.4-apache**, corresponde a la versión a instalar
* **COPY /src /var/www/html**, hace referencia a la copia de los archivos dentro de nuestro directorio que están alojados en *"/src"* a la carpeta del contenedor situada en *"/var/www/html"*.
* **EXPOSE: 80**, indica el puerto a usar.

### 3. Ejecutar el contenedor

En la terminal **ejecutar** el comando ```docker build -t hello-php .``` el cual creará una imagen leyendo el contenido del archivo Dockerfile en el directorio actual. ```-t hello-world``` asigna un tag a esa imagen. Del mismo modo descargará la imagen al completo (PHP y Apache).

El comando ```docker images``` muestra las imágenes creadas. Por un lado aparecerá *hello-php* (la imágen creada), y por otro *php* que es la imágen en la que está basada nuestro proyecto.

### 4. Ejecución de la imágen creada

```docker run -p 3000:80 hello-php```. Esto creará un contenedor a partir de la imágen *hello-php*. Le indicamos que desde nuestra máquina acceda por el puerto 3000.

Si ahora accedemos a la dirección **localhost:3000 veremos el código como se ejecuta el código creado.

Si ejecutamos ```docker run -p 3000:80 -d hello-php``` ejecutará el contenedor en modo **detached**, sin necesidad de tener la terminal abierta

### 5. Parar el contenedor

```docker ps```para ver los contenedores en ejecución y a continuación ```docker stop 43d```. Donde *43d* son los tres primeros dígitos del id del contenedor a parar.

### 6. Limpiar contenedores

```docker rm $(docker ps -aq)```. Elimina todos los contenedores (ids disponibles). Si de nuevo hacemos ```docker ps -a``` no tendremos ningún contenedor.

### 7. Uso de volúmenes

Nos permiten **copiar** contenido desde nuestro host dentro del contenedor. Para ello hacemos lo mismo que antes.

```docker run -p 5000:80 -d -v $(pwd)/src:/var/www/html/ hello-php```.

Esto permite ver en tiempo real los cambios realizados en el proyecto.

### 8. Eliminar imágenes

```docker rmi -f $(docker images -q)```

### 9. Uso de versiones y más

```docker run -p 4000:80 -d --name myserver hello-php:1.0```

### 10. Documentación oficial Docker PHP y tutoriales

* [Enlace a la documentación oficial](https://hub.docker.com/_/php/)
* [Tutorial de Fatz](https://www.youtube.com/watch?v=-XnfBItOBHE)
* [Curso Docker](https://www.youtube.com/watch?v=NVvZNmfqg6M)
* [Instalar Docker en W10](https://www.youtube.com/watch?v=BK-C2RofmTE)