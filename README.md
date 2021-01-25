# Session planning 

<img src="session.png">

## app 

<img src="appab.png">

## app deployment history and future 

<img src="appdep.png">

## Vms and containers options 

<img src="cre.png">

## info about docker 

<img src="dockerinfo.png">

## Docker installation 

<img src="dinstall.png">



## Docker Desktop URLS 

[Windows 10] ('https://hub.docker.com/editions/community/docker-ce-desktop-windows/')

---

[mac OS] ('https://hub.docker.com/editions/community/docker-ce-desktop-mac')


## installing Docker in linux vm

```
[ec2-user@ip-172-31-43-246 ~]$ sudo yum  install docker  -y
Failed to set locale, defaulting to C
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
Resolving Dependencies
--> Running transaction check
---> Package docker.x86_64 0:19.03.13ce-1.amzn2 will be installed
--> Processing Dependency: runc >= 1.0.0 for package: docker-19.03.13ce-1.amzn2.x86_64
--> Processing Dependency: containerd >= 1.3.2 for package: docker-19.03.13ce-1.amzn2.x86_64
--> Processing Dependency: pigz for package: docker-19.03.13ce-1.amzn2.x86_64
--> Processing Dependency: libcgroup for package: docker-19.03.13ce-1.amzn2.x86_64
--> Running transaction check
---> Package containerd.x86_64 0:1.4.1-2.amzn2 will be installed
---> Package libcgroup.x86_64 0:0.41-21.amzn2 will be installed
---> Package pigz.x86_64 0:2.3.4-1.amzn2.0.1 will be installed
---> Package runc.x86_64 0:1.0.0-0.1.20200826.gitff819c7.amzn2 will be installed
--> Finished Dependency Resolution


```


## starting docker 

```
[ec2-user@ip-172-31-43-246 ~]$ sudo systemctl start docker 
[ec2-user@ip-172-31-43-246 ~]$ sudo systemctl enable  docker 
Created symlink from /etc/systemd/system/multi-user.target.wants/docker.service to /usr/lib/systemd/system/docker.service.
[ec2-user@ip-172-31-43-246 ~]$ sudo systemctl status  docker 
● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; vendor preset: disabled)
   Active: active (running) since Mon 2021-01-25 05:36:59 UTC; 12s ago
     Docs: https://docs.docker.com
 Main PID: 3730 (dockerd)
   CGroup: /system.slice/docker.service
           └─3730 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock --default-ulimit nofile=10...

Jan 25 05:36:58 ip-172-31-43-246.ec2.internal dockerd[3730]: time="2021-01-25T05:36:58.118440200Z" level=info ms...rpc
Jan 25 05:36:58 ip-172-31-43-246.ec2.internal dockerd[3730]: time="2021-01-25T05:36:58.118464852Z" level=info ms...rpc
Jan 25 05:36:58 ip-172-31-43-246.ec2.internal dockerd[3730]: time="2021-01-25T05:36:58.118479537Z" level=info ms...rpc
Jan 25 05:36:58 ip-172-31-43-246.ec2.internal dockerd[3730]: time="2021-01-25T05:36:58.174346733Z" level=info ms...t."
Jan 25 05:36:58 ip-172-31-43-246.ec2.internal dockerd[3730]: time="2021-01-25T05:36:58.754972245Z" level=info ms...ss"
Jan 25 05:36:58 ip-172-31-43-246.ec2.internal dockerd[3730]: time="2021-01-25T05:36:58.958789428Z" level=info ms...e."
Jan 25 05:36:59 ip-172-31-43-246.ec2.internal dockerd[3730]: time="2021-01-25T05:36:59.023433758Z" level=info ms...-ce
Jan 25 05:36:59 ip-172-31-43-246.ec2.internal dockerd[3730]: time="2021-01-25T05:36:59.023536194Z" level=info ms...on"
Jan 25 05:36:59 ip-172-31-43-246.ec2.internal dockerd[3730]: time="2021-01-25T05:36:59.044994345Z" level=info ms...ck"
Jan 25 05:36:59 ip-172-31-43-246.ec2.internal systemd[1]: Started Docker Application Container Engine.
Hint: Some lines were ellipsized, use -l to show in full.

```

## Docker engine connecint 

```
[root@ip-172-31-43-246 ~]# useradd a
[root@ip-172-31-43-246 ~]# su - a
[a@ip-172-31-43-246 ~]$ 
[a@ip-172-31-43-246 ~]$ docker  version  
Client:
 Version:           19.03.13-ce
 API version:       1.40
 Go version:        go1.13.15
 Git commit:        4484c46
 Built:             Mon Oct 12 18:51:20 2020
 OS/Arch:           linux/amd64
 Experimental:      false
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.40/version: dial unix /var/run/docker.sock: connect: permission denied
[a@ip-172-31-43-246 ~]$ 
[a@ip-172-31-43-246 ~]$ sudo usermod -a -G docker  a 

```

## Docker client and server 

<img src="dockerarch.png">

## Docker client with multiple docker engine 

<img src="dcoptions.png">


# Searching images on Docker hub 

```
 15  docker version 
   16  docker  search  java 
   17  docker  search  python
   18  docker  search  mysql 
   19  docker  search  dockerashu
   20  docker  search  ashutoshh
   
 ```
 
 ## Docker images on docker engine 
 
 ```
    24  docker  pull  java 
   25  docker pull store/oracle/jdk:11
   26  docker  pull  java 
   27  docker  images
   28  docker  pull  python 
   29  docker pull oraclelinux
   30  docker pull oraclelinux:8.3
   31  docker images
   32  docker pull alpine 
   33  docker pull busybox 
   34  history 
[ec2-user@ip-172-31-43-246 ~]$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
alpine              latest              7731472c3f2a        10 days ago         5.61MB
oraclelinux         8.3                 f4a1f2c861ca        10 days ago         429MB
busybox             latest              b97242f89c8a        11 days ago         1.23MB
python              latest              da24d18bf4bf        12 days ago         885MB
java                latest              d23bdf5b1b1b        4 years ago         643MB

```

## image location in Docker engine server

```
Name: ip-172-31-43-246.ec2.internal
 ID: 4MIK:ZUZD:J3FL:SBMM:YOIK:Y4YP:RIPI:6VFS:4IG5:F2MS:2NBY:E6DH
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false

[ec2-user@ip-172-31-43-246 ~]$ sudo -i
[root@ip-172-31-43-246 ~]# cd  /var/lib/docker/
[root@ip-172-31-43-246 docker]# ls
builder  buildkit  containers  image  network  overlay2  plugins  runtimes  swarm  tmp  trust  volumes

```


## docker image registry options 

<img src="imgreg.png">

## container with parent process

<img src="containerpp.png">

##. first ever container 

```
[ec2-user@ip-172-31-43-246 ~]$ docker run  --name  ashuc1  alpine   ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8): 56 data bytes
64 bytes from 8.8.8.8: seq=0 ttl=112 time=1.426 ms
64 bytes from 8.8.8.8: seq=1 ttl=112 time=1.443 ms
64 bytes from 8.8.8.8: seq=2 ttl=112 time=1.685 ms
6

```

## container process

```
   45  docker run  --name  ashuc1  alpine   ping 8.8.8.8
   46  history 
[ec2-user@ip-172-31-43-246 ~]$ docker  ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[ec2-user@ip-172-31-43-246 ~]$ docker  ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS                      PORTS               NAMES
900042a2d477        alpine              "ping 8.8.8.8"      About a minute ago   Exited (0) 48 seconds ago                       ashuc1

```

## some docker command history 

```
[ec2-user@ip-172-31-43-246 ~]$ docker  ps  -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
900042a2d477        alpine              "ping 8.8.8.8"      3 minutes ago       Exited (0) 2 minutes ago                       ashuc1
[ec2-user@ip-172-31-43-246 ~]$ docker  start  ashuc1
ashuc1
[ec2-user@ip-172-31-43-246 ~]$ docker  ps  
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
e239d1e2faa7        python              "ping 8.8.8.8"      11 seconds ago      Up 10 seconds                           vivek
900042a2d477        alpine              "ping 8.8.8.8"      3 minutes ago       Up 4 seconds                            ashuc1
[ec2-user@ip-172-31-43-246 ~]$ docker  ps  
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
e239d1e2faa7        python              "ping 8.8.8.8"      31 seconds ago      Up 30 seconds                           vivek
900042a2d477        alpine              "ping 8.8.8.8"      4 minutes ago       Up 24 seconds                           ashuc1
[ec2-user@ip-172-31-43-246 ~]$ docker  stop ashuc1 
ashuc1
[ec2-user@ip-172-31-43-246 ~]$ docker  ps  
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[ec2-user@ip-172-31-43-246 ~]$ docker  start  ashuc1
ashuc1
[ec2-user@ip-172-31-43-246 ~]$ docker  ps  
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                  PORTS               NAMES
1b6ffcb3d507        java                "ping 8.8.8.8"      2 seconds ago       Up Less than a second                       venkat
900042a2d477        alpine              "ping 8.8.8.8"      5 minutes ago       Up 2 seconds                                ashuc1
[ec2-user@ip-172-31-43-246 ~]$ docker  kill  ashuc1 
ashuc1

```


## checking output of parent process 

```
  66  docker  logs  ashuc1  
   67  docker  logs  ashuc1  -f
   
```
## removing container 

```
[ec2-user@ip-172-31-43-246 ~]$ docker kill ashuc1
ashuc1
[ec2-user@ip-172-31-43-246 ~]$ docker rm  ashuc1
ashuc1

```

## best practise for launching containers

```
[ec2-user@ip-172-31-43-246 ~]$ docker run  --name ashuc2  -it  -d  alpine  ping fb.com 
1a349040cc346112dc6b3d454ddd6da7d550fd6a9eb91e133d0f74c6c7659516
[ec2-user@ip-172-31-43-246 ~]$ docker  ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
1a349040cc34        alpine              "ping fb.com"       5 seconds ago       Up 4 seconds                            ashuc2

```

## child process in running container 

```
ec2-user@ip-172-31-43-246 ~]$ 
[ec2-user@ip-172-31-43-246 ~]$ docker exec -it    ashuc3 sh 
/ # 
/ # cat  /etc/os-release 
NAME="Alpine Linux"
ID=alpine
VERSION_ID=3.13.0
PRETTY_NAME="Alpine Linux v3.13"
HOME_URL="https://alpinelinux.org/"
BUG_REPORT_URL="https://bugs.alpinelinux.org/"
/ # ps  -e
PID   USER     TIME  COMMAND
    1 root      0:00 ping google.com
    6 root      0:00 ping 8.8.8.8
   11 root      0:00 sh
   18 root      0:00 ps -e
   
 ```
 
 
