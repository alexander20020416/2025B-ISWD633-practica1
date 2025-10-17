# Operaciones con contenedores

### Ejecutar un comando en un contenedor de Docker en ejecución
```
docker exec <nombre contenedor> <comando> <argumentos opcionales>
```
```
C:\Users\ASUS TUF F15>docker exec srv-web ls /usr/share/nginx/html
50x.html
index.html
```
```
C:\Users\ASUS TUF F15>docker exec srv-web cat /usr/share/nginx/html/index.html
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

### ¿Para qué se usa el comando ls?
```
El comando ls se usa para listar los archivos y carpetas que hay dentro de un directorio. Es como cuando abres una carpeta en Windows y ves todo lo que contiene, pero en la terminal.El comando ls se usa para listar los archivos y carpetas que hay dentro de un directorio. Es como cuando abres una carpeta en Windows y ves todo lo que contiene, pero en la terminal.
```
### ¿Para qué sirve el argumento -l junto al comando ls?
```
El argumento -l hace que el listado sea más detallado. En vez de solo mostrar los nombres de los archivos, te muestra información extra como los permisos, el dueño del archivo, el tamaño, y la fecha de cuando se modificó por última vez. Básicamente te da una vista más completa de cada archivo.
```
### Usar el contenedor de jenkins creado previamente y ejecutar el comando ls con el argumento -l
```
C:\Users\ASUS TUF F15>docker exec srv-jenkins ls -l
total 56
drwxr-xr-x   1 root root 4096 Dec  5  2023 bin
drwxr-xr-x   5 root root  340 Oct 17 01:16 dev
drwxr-xr-x   1 root root 4096 Oct 17 01:16 etc
drwxr-xr-x   2 root root 4096 Nov 30  2023 home
drwxr-xr-x   1 root root 4096 Dec  5  2023 lib
drwxr-xr-x   5 root root 4096 Nov 30  2023 media
drwxr-xr-x   2 root root 4096 Nov 30  2023 mnt
drwxr-xr-x   1 root root 4096 Dec  5  2023 opt
dr-xr-xr-x 336 root root    0 Oct 17 01:16 proc
drwx------   1 root root 4096 Dec  5  2023 root
drwxr-xr-x   2 root root 4096 Nov 30  2023 run
drwxr-xr-x   1 root root 4096 Dec  5  2023 sbin
drwxr-xr-x   2 root root 4096 Nov 30  2023 srv
dr-xr-xr-x  13 root root    0 Oct 17 01:16 sys
drwxrwxrwt   1 root root 4096 Oct 17 01:16 tmp
drwxr-xr-x   1 root root 4096 Dec  5  2023 usr
drwxr-xr-x   1 root root 4096 Dec  5  2023 var
```
# COLOCAR UNA CAPTURA DE PANTALLA
<img width="976" height="393" alt="imagen" src="https://github.com/user-attachments/assets/4b6ed69a-38de-4431-85cc-0406ca3d7ee4" />

### Para ejecutar un shell interactivo en un contenedor de Docker especificado.
El comando **docker exec** te permite acceder a la sesión shell de un contenedor en ejecución, estarás dentro del contenedor y podrás ejecutar comandos como si estuvieras en una terminal normal. 
Para saber qué comando utilizar para abrir una terminal dentro de un contenedor, es útil conocer la imagen base del contenedor, ya que diferentes imágenes pueden usar diferentes shells o comandos para abrir una terminal. Puedes verificar la documentación de la imagen del contenedor en Docker Hub o en el repositorio de la imagen para obtener información específica sobre cómo abrir una terminal en esa imagen.
- Para imágenes basadas en Debian o Ubuntu, puedes probar con bash.
- Para imágenes basadas en Alpine Linux, puedes probar con sh.
![Imagen](jenkins-i.PNG)
```
docker exec -i <nombre contenedor> <programa o comando>
```
-i: mantiene abierta la entrada estándar (stdin) del contenedor. Esto significa que puedes enviar datos al proceso que se está ejecutando en el contenedor a través de la terminal local. *Sin embargo, esto no asigna un terminal al contenedor, por lo que no podrás ver la salida del proceso de forma interactiva.*

### Ejecutar una de las siguientes instrucciones
```
docker exec -i <nombre contenedor> /bin/bash 
```
ó
```
docker exec -i <nombre contenedor> bash 
```
**Considerar**
- /bin/bash: Al especificar la ruta completa del shell, Docker buscará el ejecutable /bin/bash en el sistema de archivos del contenedor y lo ejecutará. Esto es útil cuando quieres asegurarte de que se está utilizando un shell específico que está ubicado en una ubicación conocida en el sistema de archivos del contenedor. 
- bash: Al especificar solo el nombre del shell, Docker buscará el comando bash en las rutas del sistema (por lo general, en las rutas definidas en la variable de entorno PATH) del contenedor y lo ejecutará. Esto asume que bash está disponible en alguna de las rutas del sistema definidas en el contenedor.

Ejecutar
```
echo "Hola mundo"
```

Ejecutar
```
whoami
```
# COLOCAR UNA CAPTURA DE PANTALLA

**Si se visualiza el mensaje command not found, considerar**
El problema se debe a que no se ha asignado un terminal de salida al contenedor al ejecutar el comando. Cuando usas docker exec -i jenkins-server /bin/bash en Windows, el comando se ejecuta pero no hay un terminal asignado para mostrar la salida del comando ls.


### Para ejecutar un shell interactivo bidireccional en un contenedor de Docker especificado.
Ejecutar un shell interactivo bidireccional en un contenedor de Docker significa abrir una sesión de shell en el contenedor que permite la interacción bidireccional entre la terminal local y el contenedor. Es decir, puedes enviar comandos desde tu terminal local al contenedor y recibir la salida de esos comandos de vuelta en tu terminal local, al igual que si estuvieras trabajando directamente en la terminal del contenedor.

![Imagen](jenkins-it.PNG)
```
docker exec -i-t <nombre contenedor> <programa o comando>
```
ó
```
docker exec -it <nombre contenedor> <programa o comando>
```

### Ahora puedes acceder al contenedor de jenkins y obtener la contraseña ubicada en /var/jenkins_home/secrets/initialAdminPassword

# COMPLETAR

### Colocar una captura de pantalla de la ventana que aparece después de colocar la contraseña.

**Para este punto no es necesario continuar con la instalación de Jenkins**


### Para ver los logs de un contenedor

```
docker logs -n <cantidad de líneas> <nombre o id del contenedor> 
```
-t: para incluir la fecha y la hora

