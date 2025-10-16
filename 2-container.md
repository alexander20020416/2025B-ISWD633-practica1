# Contenedores

### Crear un contenedor
Para crear un nuevo contenedor Docker a partir de una imagen específica, pero sin iniciarlo automáticamente. 

```
docker create --name <nombre contenedor> <nombre imagen>:<tag>
```
Crear el contenedor  **srv-web** usando la imagen nginx version alpine
```
C:\Users\ASUS TUF F15>docker create --name srv-web nginx:alpine
18dd94b26ba136896dc1d3bdbede12740b22c86efc0acb19fe816d852c402edf
```
Si creas un contenedor en Docker sin asignarle un nombre específico utilizando la opción --name, Docker asignará automáticamente un nombre aleatorio al contenedor. Este nombre suele consistir en una combinación de palabras y números.  

Crear el contenedor usando la imagen hello-world
```
C:\Users\ASUS TUF F15>docker create hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
17eec7bbc9d7: Pull complete
Digest: sha256:6dc565aa630927052111f823c303948cf83670a3903ffa3849f1488ab517f891
Status: Downloaded newer image for hello-world:latest
487ec72ef65580e5873328abcb61968c31b0aaade2ad3e0f2634ae1de10a3b04
```
### Listar los contenedores ejecutándose o no

```
docker ps -a
```

### Para iniciar un contenedor

```
docker start <nombre contenedor o identificador>
```
Iniciar el contenedor srv-web 
```
C:\Users\ASUS TUF F15>docker start srv-web
srv-web
```
### Listar los contenedores ejecutándose
```
docker ps 
docker ps | grep <nombre contenedor>
```

### Para detener un contenedor

```
docker stop <nombre contenedor>
```

### Para crear un contenedor y ejecutarlo inmediatamente

```
docker run --name <nombre contenedor> <nombre imagen>:<tag>
```
![Ecosistema de Docker](dockerRun.PNG)

Crear y ejecutar inmediatamente el contenedor **srv-web2** usando la imagen nginx:alpine

```
C:\Users\ASUS TUF F15>docker run --name srv-web2 nginx:alpine
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2025/10/16 21:49:22 [notice] 1#1: using the "epoll" event method
2025/10/16 21:49:22 [notice] 1#1: nginx/1.29.2
2025/10/16 21:49:22 [notice] 1#1: built by gcc 14.2.0 (Alpine 14.2.0)
2025/10/16 21:49:22 [notice] 1#1: OS: Linux 6.6.87.2-microsoft-standard-WSL2
2025/10/16 21:49:22 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2025/10/16 21:49:22 [notice] 1#1: start worker processes
2025/10/16 21:49:22 [notice] 1#1: start worker process 30
2025/10/16 21:49:22 [notice] 1#1: start worker process 31
2025/10/16 21:49:22 [notice] 1#1: start worker process 32
2025/10/16 21:49:22 [notice] 1#1: start worker process 33
2025/10/16 21:49:22 [notice] 1#1: start worker process 34
2025/10/16 21:49:22 [notice] 1#1: start worker process 35
2025/10/16 21:49:22 [notice] 1#1: start worker process 36
2025/10/16 21:49:22 [notice] 1#1: start worker process 37
2025/10/16 21:49:22 [notice] 1#1: start worker process 38
2025/10/16 21:49:22 [notice] 1#1: start worker process 39
2025/10/16 21:49:22 [notice] 1#1: start worker process 40
2025/10/16 21:49:22 [notice] 1#1: start worker process 41
2025/10/16 21:49:22 [notice] 1#1: start worker process 42
2025/10/16 21:49:22 [notice] 1#1: start worker process 43
2025/10/16 21:49:22 [notice] 1#1: start worker process 44
2025/10/16 21:49:22 [notice] 1#1: start worker process 45
2025/10/16 21:49:22 [notice] 1#1: start worker process 46
2025/10/16 21:49:22 [notice] 1#1: start worker process 47
2025/10/16 21:49:22 [notice] 1#1: start worker process 48
2025/10/16 21:49:22 [notice] 1#1: start worker process 49

```

**¿Qué sucede luego de la ejecución del comando?**
```
Después de ejecutar ese comando, Docker crea un contenedor nuevo llamado srv-web2 usando la imagen nginx:alpine y arranca el servidor web Nginx dentro de él.
La terminal muestra los mensajes del inicio del servidor (como si se estuviera encendiendo).
El contenedor queda activo y corriendo Nginx, pero la terminal se queda “ocupada” mostrando los registros del servidor hasta que detengas el proceso con Ctrl + C.
```

Cuando ejecutas un contenedor en primer plano sin la opción -d (modo detach), el contenedor captura la entrada estándar (stdin) del terminal, lo que significa que el terminal queda "atrapado" y no puedes introducir más comandos hasta que detengas el contenedor.

### Para crear un contenedor y ejecutarlo inmediatamente sin estar vinculados al mismo
-d: Es la opción que indica a Docker que ejecute el contenedor en segundo plano (en modo "detach").
Cuando un contenedor se ejecuta en segundo plano, Docker devuelve el control al terminal inmediatamente después de iniciar el contenedor, lo que permite al usuario seguir ejecutando otros comandos en el mismo terminal sin que el contenedor detenga la interacción.

```
docker run -d --name <nombre contenedor> <nombre imagen>:tag
```
Crear y ejecutar inmediatamente el contenedor **srv-web3** en modo detach usando la imagen nginx:alpine
```
C:\Users\ASUS TUF F15>docker run -d --name srv-web3 nginx:alpine
6c4bf0f281e0f05e9f9214f0f1f609e296c051efa96987769ecad5ea380adfd6
```
### Para eliminar un contenedor

```
docker rm <nombre contenedor>
```
Eliminar el contenedor que se creó a partir de la imagen hello-world 
```
C:\Users\ASUS TUF F15>docker rm musing_jepsen
musing_jepsen
```
Verificar que el contenedor que se eliminó
```
C:\Users\ASUS TUF F15>docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                      PORTS     NAMES
6c4bf0f281e0   nginx:alpine   "/docker-entrypoint.…"   6 minutes ago    Up 6 minutes                80/tcp    srv-web3
b1d76125e6b3   nginx:alpine   "/docker-entrypoint.…"   14 minutes ago   Exited (0) 7 minutes ago              srv-web2
18dd94b26ba1   nginx:alpine   "/docker-entrypoint.…"   30 minutes ago   Exited (0) 16 minutes ago             srv-web
```
### Para eliminar un contenedor que esté ejecutándose

```
docker rm -f <nombre contenedor>
```
Eliminar el contenedor **srv-web3** 
```
C:\Users\ASUS TUF F15>docker rm srv-web3
srv-web3
```
Verificar que el contenedor que se eliminó
```
C:\Users\ASUS TUF F15>docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                      PORTS     NAMES
b1d76125e6b3   nginx:alpine   "/docker-entrypoint.…"   17 minutes ago   Exited (0) 11 minutes ago             srv-web2
18dd94b26ba1   nginx:alpine   "/docker-entrypoint.…"   33 minutes ago   Exited (0) 20 minutes ago             srv-web
```
### Para inspecionar un contenedor 

Inspeccionar el contenedor **srv-web** 
# COMPLETAR
```
C:\Users\ASUS TUF F15>docker inspect srv-web
[
    {
        "Id": "18dd94b26ba136896dc1d3bdbede12740b22c86efc0acb19fe816d852c402edf",
        "Created": "2025-10-16T21:33:09.762747771Z",
        "Path": "/docker-entrypoint.sh",
        "Args": [
            "nginx",
            "-g",
            "daemon off;"
        ],
        "State": {
            "Status": "exited",
            "Running": false,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 0,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2025-10-16T21:42:29.386712729Z",
            "FinishedAt": "2025-10-16T21:46:44.011989732Z"
        },
        "Image": "sha256:61e01287e546aac28a3f56839c136b31f590273f3b41187a36f46f6a03bbfe22",
        "ResolvConfPath": "/var/lib/docker/containers/18dd94b26ba136896dc1d3bdbede12740b22c86efc0acb19fe816d852c402edf/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/18dd94b26ba136896dc1d3bdbede12740b22c86efc0acb19fe816d852c402edf/hostname",
        "HostsPath": "/var/lib/docker/containers/18dd94b26ba136896dc1d3bdbede12740b22c86efc0acb19fe816d852c402edf/hosts",
        "LogPath": "/var/lib/docker/containers/18dd94b26ba136896dc1d3bdbede12740b22c86efc0acb19fe816d852c402edf/18dd94b26ba136896dc1d3bdbede12740b22c86efc0acb19fe816d852c402edf-json.log",
        "Name": "/srv-web",
        "RestartCount": 0,
        "Driver": "overlayfs",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "bridge",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "ConsoleSize": [
                30,
                120
            ],
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "private",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": [],
            "BlkioDeviceWriteBps": [],
            "BlkioDeviceReadIOps": [],
            "BlkioDeviceWriteIOps": [],
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": null,
            "PidsLimit": null,
            "Ulimits": [],
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/interrupts",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware",
                "/sys/devices/virtual/powercap"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": null,
            "Name": "overlayfs"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "18dd94b26ba1",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": true,
            "AttachStderr": true,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.29.2",
                "PKG_RELEASE=1",
                "DYNPKG_RELEASE=1",
                "NJS_VERSION=0.9.3",
                "NJS_RELEASE=1"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "Image": "nginx:alpine",
            "Volumes": null,
            "WorkingDir": "/",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {
                "maintainer": "NGINX Docker Maintainers \u003cdocker-maint@nginx.com\u003e"
            },
            "StopSignal": "SIGQUIT",
            "StopTimeout": 1
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "",
            "SandboxKey": "",
            "Ports": {},
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "",
            "Gateway": "",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "",
            "IPPrefixLen": 0,
            "IPv6Gateway": "",
            "MacAddress": "",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "MacAddress": "",
                    "DriverOpts": null,
                    "GwPriority": 0,
                    "NetworkID": "88738dc90424e85cfb8313838e61da6592cb7e393e8834869c62528de40e51b5",
                    "EndpointID": "",
                    "Gateway": "",
                    "IPAddress": "",
                    "IPPrefixLen": 0,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "DNSNames": null
                }
            }
        },
        "ImageManifestDescriptor": {
            "mediaType": "application/vnd.oci.image.manifest.v1+json",
            "digest": "sha256:b03ccb7431a2e3172f5cbae96d82bd792935f33ecb88fbf2940559e475745c4e",
            "size": 2495,
            "annotations": {
                "com.docker.official-images.bashbrew.arch": "amd64",
                "org.opencontainers.image.base.digest": "sha256:42b8c29407145d2c4445befb4cdd7bccaecc67c00dd20762c3ee40dbe9587e3f",
                "org.opencontainers.image.base.name": "nginx:1.29.2-alpine-slim",
                "org.opencontainers.image.created": "2025-10-08T23:33:31Z",
                "org.opencontainers.image.revision": "c3785f2653008f9354c3d29a54d8c5459c53fa60",
                "org.opencontainers.image.source": "https://github.com/nginx/docker-nginx.git#c3785f2653008f9354c3d29a54d8c5459c53fa60:mainline/alpine",
                "org.opencontainers.image.url": "https://hub.docker.com/_/nginx",
                "org.opencontainers.image.version": "1.29.2-alpine"
            },
            "platform": {
                "architecture": "amd64",
                "os": "linux"
            }
        }
    }
]
```
