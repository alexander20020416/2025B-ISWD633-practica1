# Lo que aprendí sobre Docker

## Trabajando con imágenes

Primero que nada, aprendí que para bajar una imagen de Docker uso el comando `docker pull`. Si no le pongo ninguna versión específica, automáticamente me trae la última versión disponible (la que tiene el tag "latest").

Por ejemplo, cuando descargué nginx en su versión alpine quedó algo así:
```
docker pull nginx:alpine
```

Para ver todas las imágenes que tengo en mi computadora, simplemente uso `docker images` y me sale una lista con toda la info: el nombre, el tag, el ID y el tamaño.

También descubrí que puedo inspeccionar una imagen con `docker inspect` para ver toda su información detallada en formato JSON. Algo interesante que noté es que el ID de las imágenes se genera con SHA-256, que es un algoritmo bastante seguro.

## Creando y manejando contenedores

Hay varias formas de trabajar con contenedores. Puedo crear uno sin que se ejecute usando `docker create`, o crearlo y arrancarlo de una vez con `docker run`.

Lo que más me llamó la atención fue la diferencia entre ejecutar un contenedor normal y uno en modo "detach". Cuando lo haces sin el `-d`, la terminal se queda pegada mostrando los logs del contenedor y no puedes hacer nada más. Pero si le pones el `-d`, el contenedor corre en segundo plano y recuperas el control de la terminal inmediatamente.

Para ver los contenedores uso `docker ps` (solo los que están corriendo) o `docker ps -a` (todos, incluso los detenidos).

## Mapeo de puertos

Esta parte me pareció súper importante. Básicamente, el mapeo de puertos me permite acceder desde mi navegador a servicios que están corriendo dentro del contenedor. 

La estructura es así:
```
docker run -d --name mi-contenedor -p puerto-host:puerto-contenedor imagen:tag
```

Por ejemplo, cuando monté nginx con el puerto 3000 en mi máquina apuntando al puerto 80 del contenedor, pude entrar desde `http://localhost:3000` y ver la página de bienvenida de nginx.

También aprendí que puedo mapear varios puertos a la vez, como hice con RabbitMQ que necesitaba el 5672 y el 15672.

## Ejecutando comandos dentro de contenedores

Con `docker exec` puedo ejecutar comandos dentro de un contenedor que ya está corriendo. Esto es muy útil para ver qué hay adentro o hacer cambios.

Si solo quiero ejecutar un comando rápido:
```
docker exec nombre-contenedor comando
```

Pero si quiero entrar al contenedor como si estuviera en una terminal normal, necesito usar `-it`:
```
docker exec -it nombre-contenedor bash
```

El `-i` mantiene abierta la entrada y el `-t` asigna un terminal. Juntos me permiten trabajar de forma interactiva dentro del contenedor.

## Viendo los logs

Para revisar qué está pasando dentro de un contenedor uso `docker logs`. Puedo limitar la cantidad de líneas con `-n` y si quiero ver los logs en tiempo real le pongo `-f`.

## Cosas importantes que aprendí

- No puedo agregar mapeo de puertos a un contenedor que ya existe, tengo que definirlos cuando lo creo
- Cuando elimino una imagen, los contenedores que se crearon de ella no se eliminan automáticamente
- Es mejor detener los contenedores antes de eliminar las imágenes para evitar problemas
- El comando `ls` lista archivos y con `-l` me da más detalles como permisos, tamaño y fecha
- Para salir de un contenedor interactivo uso `exit` o Ctrl+D

## Práctica con Jenkins

Monté un servidor Jenkins y aprendí a obtener la contraseña inicial que está guardada en un archivo dentro del contenedor. Usé:
```
docker exec srv-jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

Esto me dio la contraseña que necesitaba para acceder por primera vez a la interfaz web de Jenkins.
