# Mapeo de puertos
El mapeo de puertos es un mecanismo que permite redirigir el tráfico de red desde un puerto en el host (tu máquina local o servidor) hacia un puerto específico en un contenedor Docker.
Por ejemplo, supongamos que tienes un contenedor que ejecuta un servidor web en el puerto 80 dentro del contenedor, pero quieres acceder a ese servidor desde tu navegador en la máquina host. Puedes usar el mapeo de puertos para redirigir el tráfico del puerto 80 del contenedor al puerto 3000 en el host. De esta manera, cuando accedas a http://localhost:3000 en tu navegador, el tráfico se dirigirá al servidor web dentro del contenedor en el puerto 80.

![mapeo](mapeoPuertos.PNG)

### Para crear un mapeo de puertos (puerto host y puerto contenedor)
El mapeo de puertos se especifica al ejecutar un contenedor Docker utilizando la opción -p o --publish seguida de los puertos que deseas mapear
```
docker run -d --name <nombre contenedor> -p <puerto host>:<puerto contenedor> <nombre imagen>:<tag>

```
Crear un contenedor a partir de la imagen nginx version alpine con el mapeo de puertos del ejemplo gráfico, host 3000 y contenedor 80
```
C:\Users\ASUS TUF F15>docker run -d --name srv-web -p 3000:80 nginx:alpine
dfefbda00c44b2e46a433a02b715391bbc05e715e139471f168df10d0a0ecac2
```
# COLOCAR UNA CAPTURA DE PANTALLA  DEL ACCESO http://localhost:3000
<img width="1920" height="912" alt="imagen" src="https://github.com/user-attachments/assets/82135972-b6a4-4b5c-83b6-914aa31934db" />

### Para mapear más de un puerto

```
docker run -d --name <nombre contenedor> -p <puerto host 01>:<puerto contenedor 01> -p <puerto host 02>:<puerto contenedor 02> <nombre imagen>:<tag>
```

Crear un contenedor a partir de la imagen rabbitmq version management-alpine, para este mapeo de puertos usar en el host los mismos puertos del contenedor.
```
C:\Users\ASUS TUF F15>docker run -d --name srv-rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:management-alpine
Unable to find image 'rabbitmq:management-alpine' locally
management-alpine: Pulling from library/rabbitmq
e4735dbf282e: Pull complete
fb346a2cdaaf: Pull complete
7067fd18a1bb: Pull complete
502259fb5ecb: Pull complete
58ba89a44c55: Pull complete
e48767f73009: Pull complete
093d2fc1bf3f: Pull complete
f813d1ca6a64: Pull complete
9cfbd257abed: Pull complete
Digest: sha256:5cbd7145b0306399ad68422c3350b6cbd1bb95704b39f5896480e5b6d4238a04
Status: Downloaded newer image for rabbitmq:management-alpine
01e95e7db672908e08f16c0f71a2b831a0e2f1f38f61b52b8c549582db90176a
```
```
<img width="1920" height="912" alt="imagen" src="https://github.com/user-attachments/assets/bff9b727-d50d-4aa9-b199-f238a6b65b11" />
```
### Usando una forma más semántica cuando se especifican puertos

```
docker run -d --name <nombre contenedor> --publish published=<valorPuertoHost>,target=<valor> <nombre imagen>:<tag> 
```
### Publicando todos los puertos
```
docker run -P -d --name <nombre contenedor> <nombre imagen>:<tag> 
```

-P: le indica a Docker que asigne automáticamente puertos aleatorios en tu host para todos los puertos expuestos por el contenedor.

**Recordar**
No puedes mapear puertos a un contenedor existente directamente después de su creación con Docker. El mapeo de puertos debe especificarse en el momento de crear y ejecutar el contenedor.

### Crear contenedor de Jenkins puertos contenedor: 8080 (interface web) y 50000 (comunicación entre nodos) imagen: jenkins/jenkins:alpine3.18-jdk11
```
C:\Users\ASUS TUF F15>docker run -d --name srv-jenkins --publish published=8080,target=8080 --publish published=50000,target=50000 jenkins/jenkins:alpine3.18-jdk11
Unable to find image 'jenkins/jenkins:alpine3.18-jdk11' locally
alpine3.18-jdk11: Pulling from jenkins/jenkins
064a3e26f4c3: Pull complete
1c5813922572: Pull complete
8c8b33a11025: Pull complete
0f92a263615f: Pull complete
a97ebf1389b9: Pull complete
45f7db6458a9: Pull complete
c4d0d28b6211: Pull complete
c926b61bad3b: Pull complete
0425be0277df: Pull complete
12edf75a8110: Pull complete
8034e9541195: Pull complete
f53b573d02cc: Pull complete
Digest: sha256:3aeedd41d77f5f8284b77e7bfef5e10bcb3f57c57aa70a0034b90356300bb058
Status: Downloaded newer image for jenkins/jenkins:alpine3.18-jdk11
1734130c1dbb58125bb21526e0fd603bdd04a21d1945e7e1bfe2122592275054
```
# COLOCAR UNA CAPTURA DE PANTALLA  DEL ACCESO http://localhost:8080

<img width="1920" height="912" alt="imagen" src="https://github.com/user-attachments/assets/b54c9250-1b94-445f-90f8-d1bdc54dc437" />

### ¿Cómo obtener la contraseña solicitada?
Para obtener la contraseña solicitada es necesario ingresar al contenedor.

![Imagen](jenkins.PNG)
```
C:\Users\ASUS TUF F15>docker exec srv-jenkins cat /var/jenkins_home/secrets/initialAdminPassword
89b29db99aa846f19b508df6364675bf
```
