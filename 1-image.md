# Imagen
### Descargar imagen
Descarga la última versión de la imagen disponible en el registro de Docker.

```
docker pull <nombre imagen> 
```

Descarga una versión específica de la imagen, cada imagen tiene etiquetas (tags) para diferentes versiones.
Una imagen puede tener la etiqueta latest para representar la última versión, si no se especifica una etiqueta se hará referencia a la versión latest.

```
docker pull <nombre imagen>:<tag>
```

Descargar la imagen **hello-world**
C:\Users\ASUS TUF F15>docker pull hello-world
Using default tag: latest
latest: Pulling from library/hello-world
17eec7bbc9d7: Pull complete
Digest: sha256:6dc565aa630927052111f823c303948cf83670a3903ffa3849f1488ab517f891
Status: Downloaded newer image for hello-world:latest
docker.io/library/hello-world:latest

**¿Qué es nginx**
Es un servidor web de alto rendimiento que también puede funcionar como:
Servidor proxy inverso (redirige peticiones a otros servidores, útil para balancear carga o proteger servicios internos).
Balanceador de carga (distribuye las solicitudes entre varios servidores para mejorar rendimiento y disponibilidad).
Servidor de correo (IMAP/POP3/SMTP proxy) en algunos casos.
Servidor de contenido estático (imágenes, CSS, JavaScript, archivos).


Descargar la imagen  **nginx** en la versión **alpine**
C:\Users\ASUS TUF F15>docker pull nginx:alpine
alpine: Pulling from library/nginx
76c9bcaa4163: Pull complete
83ce83cd9960: Pull complete
7fb80c2f28bc: Pull complete
f80aba050ead: Pull complete
03e63548f209: Pull complete
621a51978ed7: Pull complete
e2d0ea5d3690: Pull complete
2d35ebdb57d9: Pull complete
Digest: sha256:61e01287e546aac28a3f56839c136b31f590273f3b41187a36f46f6a03bbfe22
Status: Downloaded newer image for nginx:alpine
docker.io/library/nginx:alpine

### Listar imágenes

```
docker images
```

<img width="737" height="103" alt="imagen" src="https://github.com/user-attachments/assets/32347538-89e3-4429-b9a4-e371b8816407" />


**Identificadores**

En Docker, se utilizan varios identificadores para diferenciar de manera única los elementos del sistema, como imágenes, contenedores, volúmenes y redes. Estos identificadores son generados automáticamente por Docker y son únicos dentro del contexto del sistema Docker en el que se encuentran. 

### Inspeccionar una imagen
El comando docker inspect se utiliza para obtener información detallada sobre un objeto de Docker específico, como un contenedor, una imagen, un volumen o una red.  Proporciona información en formato JSON sobre el objeto especificado.

```
docker inspect <nombre imagen>
docker inspect <nombre imagen>:<tag>
```

Inspeccionar la imagen hello-world 
# COMPLETAR

**¿Con qué algoritmo se está generando el ID de la imagen**
# COMPLETAR

### Filtrar imágenes

```
docker images | grep <termino a buscar>

```

### Para eliminar una imagen
Eliminar permanentemente la imagen de tu sistema Docker.

```
docker rmi <nombre imagen>:<tag>
```

Eliminar la imagen hello-world 
# COMPLETAR

-f: Es la opción para forzar la eliminación de la imagen incluso si hay contenedores en ejecución que utilizan esa imagen.
Cuando eliminas una imagen Docker, Docker no elimina automáticamente los contenedores que se han creado a partir de esa imagen. Esto significa que, aunque hayas eliminado la imagen, el contenedor seguirá ejecutándose normalmente.  
**Considerar**
Eliminar una imagen no afecta a los contenedores que se han creado a partir de esa imagen, a menos que esos contenedores dependan de archivos o configuraciones específicas de la imagen eliminada. En ese caso, es posible que los contenedores se comporten de manera inesperada después de eliminar la imagen.
Es una buena práctica detener y eliminar todos los contenedores que dependan de una imagen antes de eliminar la imagen en sí.

```
docker rmi -f <nombre imagen>:<tag>
```
