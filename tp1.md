# I. Init

## 3. sudo c pa bo

### 🌞 Ajouter votre utilisateur au groupe docker

```
sudo usermod -aG docker danyg
```

## 4. Un premier conteneur en vif

### 🌞 Lancer un conteneur NGINX

```
danyg@danygThinkPad:~$ docker run -d -p 9999:80 nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
bc0965b23a04: Pull complete 
650ee30bbe5e: Pull complete 
8cc1569e58f5: Pull complete 
362f35df001b: Pull complete 
13e320bf29cd: Pull complete 
7b50399908e1: Pull complete 
57b64962dd94: Pull complete 
Digest: sha256:fb197595ebe76b9c0c14ab68159fd3c08bd067ec62300583543f0ebda353b5be
Status: Downloaded newer image for nginx:latest
db2426f8b8e89e7599c2ce16ed2603eea13006e7f1024b755f3192905e4e85b9
```

### 🌞 Visitons

- vérifier que le conteneur est actif avec une commande qui liste les conteneurs en cours de fonctionnement
```
danyg@danygThinkPad:~$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                                     NAMES
db2426f8b8e8   nginx     "/docker-entrypoint.…"   7 minutes ago   Up 7 minutes   0.0.0.0:9999->80/tcp, [::]:9999->80/tcp   trusting_bartik
```

- afficher les logs du conteneur

```
danyg@danygThinkPad:~$ docker logs db
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/12/11 14:30:53 [notice] 1#1: using the "epoll" event method
2024/12/11 14:30:53 [notice] 1#1: nginx/1.27.3
2024/12/11 14:30:53 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14) 
2024/12/11 14:30:53 [notice] 1#1: OS: Linux 6.8.0-49-generic
2024/12/11 14:30:53 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2024/12/11 14:30:53 [notice] 1#1: start worker processes
2024/12/11 14:30:53 [notice] 1#1: start worker process 28
2024/12/11 14:30:53 [notice] 1#1: start worker process 29
2024/12/11 14:30:53 [notice] 1#1: start worker process 30
2024/12/11 14:30:53 [notice] 1#1: start worker process 31
2024/12/11 14:30:53 [notice] 1#1: start worker process 32
2024/12/11 14:30:53 [notice] 1#1: start worker process 33
2024/12/11 14:30:53 [notice] 1#1: start worker process 34
2024/12/11 14:30:53 [notice] 1#1: start worker process 35
```

- afficher toutes les informations relatives au conteneur avec une commande docker inspect

```
danyg@danygThinkPad:~$ docker inspect db
[
    {
        "Id": "db2426f8b8e89e7599c2ce16ed2603eea13006e7f1024b755f3192905e4e85b9",
        "Created": "2024-12-11T14:30:52.476761012Z",
        "Path": "/docker-entrypoint.sh",
        "Args": [
            "nginx",
            "-g",
            "daemon off;"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 8994,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2024-12-11T14:30:53.113433275Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:66f8bdd3810c96dc5c28aec39583af731b34a2cd99471530f53c8794ed5b423e",
        "ResolvConfPath": "/var/lib/docker/containers/db2426f8b8e89e7599c2ce16ed2603eea13006e7f1024b755f3192905e4e85b9/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/db2426f8b8e89e7599c2ce16ed2603eea13006e7f1024b755f3192905e4e85b9/hostname",
        "HostsPath": "/var/lib/docker/containers/db2426f8b8e89e7599c2ce16ed2603eea13006e7f1024b755f3192905e4e85b9/hosts",
        "LogPath": "/var/lib/docker/containers/db2426f8b8e89e7599c2ce16ed2603eea13006e7f1024b755f3192905e4e85b9/db2426f8b8e89e7599c2ce16ed2603eea13006e7f1024b755f3192905e4e85b9-json.log",
        "Name": "/trusting_bartik",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "docker-default",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "bridge",
            "PortBindings": {
                "80/tcp": [
                    {
                        "HostIp": "",
                        "HostPort": "9999"
                    }
                ]
            },
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "ConsoleSize": [
                21,
                190
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
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/e3f318dc4a573bf0a6c748fb6973ecc8fe0a09e1e3f3f26387dab923717b1008-init/diff:/var/lib/docker/overlay2/732ac81a2eba780838b751aad697d884a092905a5f6a7b515b77c7192365587a/diff:/var/lib/docker/overlay2/67f7c62cdb7d7421a00025f4a5400dfcdde5126f38054ba4b1142e521a671bc9/diff:/var/lib/docker/overlay2/fe884f560e8456d8c13e313290520ff9483f40ce494c941dc1888ffd40d71709/diff:/var/lib/docker/overlay2/3be8a9e6039c73fcdbb35b79dd823a17cc82d3d7ea515c63999410eb224c5caa/diff:/var/lib/docker/overlay2/72b9c27ecc6e6f4aaadbbdca651a409cdd28c399b0218b10134473d305a4c876/diff:/var/lib/docker/overlay2/7f28908bc699dcafcc97e4145804ae20ee58c7778aed76f7bf5a72b3eb175bc2/diff:/var/lib/docker/overlay2/93911ad3dcbb6ca5c660eb4aa4b0f654442218c345d86cebdcc87cedb5353311/diff",
                "MergedDir": "/var/lib/docker/overlay2/e3f318dc4a573bf0a6c748fb6973ecc8fe0a09e1e3f3f26387dab923717b1008/merged",
                "UpperDir": "/var/lib/docker/overlay2/e3f318dc4a573bf0a6c748fb6973ecc8fe0a09e1e3f3f26387dab923717b1008/diff",
                "WorkDir": "/var/lib/docker/overlay2/e3f318dc4a573bf0a6c748fb6973ecc8fe0a09e1e3f3f26387dab923717b1008/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "db2426f8b8e8",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.27.3",
                "NJS_VERSION=0.8.7",
                "NJS_RELEASE=1~bookworm",
                "PKG_RELEASE=1~bookworm",
                "DYNPKG_RELEASE=1~bookworm"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "Image": "nginx",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {
                "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>"
            },
            "StopSignal": "SIGQUIT"
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "2ccb8cecb19b4a1b3f120d74a41942d94173b3c0a49879ba1b4459bda3ec902b",
            "SandboxKey": "/var/run/docker/netns/2ccb8cecb19b",
            "Ports": {
                "80/tcp": [
                    {
                        "HostIp": "0.0.0.0",
                        "HostPort": "9999"
                    },
                    {
                        "HostIp": "::",
                        "HostPort": "9999"
                    }
                ]
            },
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "e1fd9bc8de576e0d5f7f8b7ea5f9a5ba6a8ada881ee98f4c2d2436cbca98d501",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null,
                    "NetworkID": "3078a6e38528e733c5fb11d0b96847d68a096927d555ed4c9c410c00ceec7aad",
                    "EndpointID": "e1fd9bc8de576e0d5f7f8b7ea5f9a5ba6a8ada881ee98f4c2d2436cbca98d501",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "DNSNames": null
                }
            }
        }
    }
]
```

- afficher le port en écoute sur la VM avec un sudo ss -lnpt

```
danyg@danygThinkPad:~$ sudo ss -lnpt | grep docker
LISTEN 0      4096              0.0.0.0:9999       0.0.0.0:*    users:(("docker-proxy",pid=8922,fd=4))                                                                                                                                                                                         
LISTEN 0      4096                 [::]:9999          [::]:*    users:(("docker-proxy",pid=8928,fd=4))                                                                                                                                                                  
```
- ouvrir le port 9999/tcp (vu dans le ss au dessus normalement) dans le firewall de la VM

```
danyg@danygThinkPad:~$ iptables -A INPUT -p TCP --dport 9999 -j ACCEPT
```
- depuis le navigateur de votre PC, visiter le site web sur http://IP_VM:9999
```
danyg@danygThinkPad:~$ curl http://172.17.0.1:9999
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
### 🌞 On va ajouter un site Web au conteneur NGINX

```
danyg@danygThinkPad:~/nginx$ docker run -d -p 9999:8080 -v /home/danyg/nginx/index.html:/var/www/html/index.html -v /home/danyg/nginx/site_nul.conf:/etc/nginx/conf.d/site_nul.conf nginx
64a896b84f05319da04fa224d7a1df99672efeb1d49bc7e7f5c6e1500593801c
```

### 🌞 Visitons

- vérifier que le conteneur est actif

```
danyg@danygThinkPad:~/nginx$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                                                 NAMES
64a896b84f05   nginx     "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes   80/tcp, 0.0.0.0:9999->8080/tcp, [::]:9999->8080/tcp   affectionate_knuth
```

- visiter le site web depuis votre PC

```
danyg@danygThinkPad:~/nginx$ curl http://172.17.0.1:9999
<h1>caca</h1>
```
## 5. Un deuxième conteneur en vif

### 🌞 Lance un conteneur Python, avec un shell


```
danyg@danygThinkPad:~/nginx$ docker run -it python bash
Unable to find image 'python:latest' locally
latest: Pulling from library/python
fdf894e782a2: Pull complete 
5bd71677db44: Pull complete 
551df7f94f9c: Pull complete 
ce82e98d553d: Pull complete 
5f0e19c475d6: Pull complete 
abab87fa45d0: Pull complete 
2ac2596c631f: Pull complete 
Digest: sha256:220d07595f288567bbf07883576f6591dad77d824dce74f0c73850e129fa1f46
Status: Downloaded newer image for python:latest
root@def0a06f56ce:/# 
```
### 🌞 Installe des libs Python

```
root@def0a06f56ce:/# pip install aiohttp
Collecting aiohttp
  Downloading aiohttp-3.11.10-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (7.7 kB)
Collecting aiohappyeyeballs>=2.3.0 (from aiohttp)
  Downloading aiohappyeyeballs-2.4.4-py3-none-any.whl.metadata (6.1 kB)
Collecting aiosignal>=1.1.2 (from aiohttp)
  Downloading aiosignal-1.3.1-py3-none-any.whl.metadata (4.0 kB)
Collecting attrs>=17.3.0 (from aiohttp)
  Downloading attrs-24.2.0-py3-none-any.whl.metadata (11 kB)
Collecting frozenlist>=1.1.1 (from aiohttp)
  Downloading frozenlist-1.5.0-cp313-cp313-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (13 kB)
Collecting multidict<7.0,>=4.5 (from aiohttp)
  Downloading multidict-6.1.0-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (5.0 kB)
Collecting propcache>=0.2.0 (from aiohttp)
  Downloading propcache-0.2.1-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (9.2 kB)
Collecting yarl<2.0,>=1.17.0 (from aiohttp)
  Downloading yarl-1.18.3-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (69 kB)
Collecting idna>=2.0 (from yarl<2.0,>=1.17.0->aiohttp)
  Downloading idna-3.10-py3-none-any.whl.metadata (10 kB)
Downloading aiohttp-3.11.10-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.7 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.7/1.7 MB 35.0 MB/s eta 0:00:00
Downloading aiohappyeyeballs-2.4.4-py3-none-any.whl (14 kB)
Downloading aiosignal-1.3.1-py3-none-any.whl (7.6 kB)
Downloading attrs-24.2.0-py3-none-any.whl (63 kB)
Downloading frozenlist-1.5.0-cp313-cp313-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (267 kB)
Downloading multidict-6.1.0-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (131 kB)
Downloading propcache-0.2.1-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (227 kB)
Downloading yarl-1.18.3-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (339 kB)
Downloading idna-3.10-py3-none-any.whl (70 kB)
Installing collected packages: propcache, multidict, idna, frozenlist, attrs, aiohappyeyeballs, yarl, aiosignal, aiohttp
Successfully installed aiohappyeyeballs-2.4.4 aiohttp-3.11.10 aiosignal-1.3.1 attrs-24.2.0 frozenlist-1.5.0 idna-3.10 multidict-6.1.0 propcache-0.2.1 yarl-1.18.3
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager, possibly rendering your system unusable.It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv. Use the --root-user-action option if you know what you are doing and want to suppress this warning.
root@def0a06f56ce:/# pip install aioconsole
Collecting aioconsole
  Downloading aioconsole-0.8.1-py3-none-any.whl.metadata (46 kB)
Downloading aioconsole-0.8.1-py3-none-any.whl (43 kB)
Installing collected packages: aioconsole
Successfully installed aioconsole-0.8.1
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager, possibly rendering your system unusable.It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv. Use the --root-user-action option if you know what you are doing and want to suppress this warning.
root@def0a06f56ce:/# python
Python 3.13.1 (main, Dec  4 2024, 20:40:27) [GCC 12.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import aiohttp
>>> 
```

# II. Images

## 1. Images publiques

### 🌞 Récupérez des images

```
danyg@danygThinkPad:~$ docker image ls
REPOSITORY           TAG       IMAGE ID       CREATED         SIZE
linuxserver/wikijs   latest    863e49d2e56c   5 days ago      465MB
python               latest    3ca4060004b1   7 days ago      1.02GB
python               3.11      342f2c43d207   7 days ago      1.01GB
nginx                latest    66f8bdd3810c   2 weeks ago     192MB
wordpress            latest    c89b40a25cd1   2 weeks ago     700MB
mysql                5.7       5107333e08a8   12 months ago   501MB
hello-world          latest    d2c94e258dcb   19 months ago   13.3kB
```
### 🌞 Lancez un conteneur à partir de l'image Python

```
danyg@danygThinkPad:~$ docker run -it python:3.11 bash
root@8bd9968e4642:/# 
```

## 2. Construire une image

### 🌞 Ecrire un Dockerfile pour une image qui héberge une application Python

```
danyg@danygThinkPad:~/python_app_build$ cat Dockerfile 
FROM debian
RUN apt update
RUN apt install -y python3
RUN pip install emoji
COPY app.py /
ENTRYPOINT ["python3", "app.py"]
```
### 🌞 Build l'image

```
danyg@danygThinkPad:~/python_app_build$ docker build . -t python_app:version_de_ouf
[+] Building 0.8s (9/9) FINISHED                                               docker:default
 => [internal] load build definition from Dockerfile                                     0.0s
 => => transferring dockerfile: 145B                                                     0.0s
 => [internal] load metadata for docker.io/library/debian:latest                         0.4s
 => [internal] load .dockerignore                                                        0.0s
 => => transferring context: 2B                                                          0.0s
 => [1/4] FROM docker.io/library/debian:latest@sha256:17122fe3d66916e55c0cbd5bbf54bb3f8  0.0s
 => [internal] load build context                                                        0.0s
 => => transferring context: 27B                                                         0.0s
 => CACHED [2/4] RUN apt-get update                                                      0.0s
 => CACHED [3/4] RUN apt install -y python3.11                                           0.0s
 => [4/4] COPY app.py /                                                                  0.0s
 => exporting to image                                                                   0.3s
 => => exporting layers                                                                  0.3s
 => => writing image sha256:b5c28273acce2842afdef038c4be82d9319e776a8ee77bd2e6b21327609  0.0s
 => => naming to docker.io/library/python_app:version_de_ouf                    
```

### 🌞 Lancer l'image


# III. Docker compose

### 🌞 Créez un fichier docker-compose.yml

```
danyg@danygThinkPad:~/compose_test$ cat docker-compose.yml 
version: "3"

services:
  conteneur_nul:
    image: debian
    entrypoint: sleep 9999
  conteneur_flopesque:
    image: debian
    entrypoint: sleep 9999
```
### 🌞 Lancez les deux conteneurs avec docker compose

```
danyg@danygThinkPad:~/compose_test$ docker compose up -d
WARN[0000] /home/danyg/compose_test/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
[+] Running 3/3
 ✔ conteneur_nul Pulled                                                                  2.9s 
 ✔ conteneur_flopesque Pulled                                                            2.6s 
   ✔ fdf894e782a2 Already exists                                                         0.0s 
[+] Running 3/3
 ✔ Network compose_test_default                  Creat...                                0.1s 
 ✔ Container compose_test-conteneur_flopesque-1  Started                                 0.3s 
 ✔ Container compose_test-conteneur_nul-1        Started                                 0.3s 
```
### 🌞 Vérifier que les deux conteneurs tournent

```
danyg@danygThinkPad:~/compose_test$ docker compose ps
WARN[0000] /home/danyg/compose_test/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
NAME                                 IMAGE     COMMAND        SERVICE               CREATED              STATUS              PORTS
compose_test-conteneur_flopesque-1   debian    "sleep 9999"   conteneur_flopesque   About a minute ago   Up About a minute   
compose_test-conteneur_nul-1         debian    "sleep 9999"   conteneur_nul         About a minute ago   Up About a minute   
```
### 🌞 Pop un shell dans le conteneur conteneur_nul

```
danyg@danygThinkPad:~/compose_test$ docker compose exec conteneur_nul bash
WARN[0000] /home/danyg/compose_test/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
root@9f7e8b60e40a:/# ping conteneur_lopesque
bash: ping: command not found
root@9f7e8b60e40a:/# 
```
