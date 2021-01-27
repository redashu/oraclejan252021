# Dockerfile More example 

## java web app using tomcat 

### web server info 

<img src="webinfo.png">

## tomcat 

```
❯ ls
README.md       ashu.dockerfile myapp
❯ cat  ashu.dockerfile
FROM tomcat 
# we are using standard docker image from Docker hub 
MAINTAINER  ashutoshh
WORKDIR /usr/local/tomcat/webapps
# changing directory 
RUN mkdir app
WORKDIR app
ADD myapp  . 
#  add and copy both are same in dockerfile while add can except data from URL as well
RUN chmod 755  . -R

```
## building tomcat web image

```
❯ docker build  -t  tomcat:ashuv1 -f  ashu.dockerfile  .
Sending build context to Docker daemon  102.9kB
Step 1/8 : FROM tomcat
 ---> 345867df0879
Step 2/8 : MAINTAINER  ashutoshh
 ---> Using cache
 ---> 4f19547d56ff
Step 3/8 : WORKDIR /usr/local/tomcat/webapps
 ---> Using cache
 ---> 93a75a0c054b
Step 4/8 : RUN mkdir app
 ---> Using cache
 ---> 05e77f22df43
Step 5/8 : WORKDIR app
 ---> Using cache
 ---> d18b7c8b41c2
Step 6/8 : ADD myapp  .
 ---> Using cache
 ---> c5c6dde1dc0b
Step 7/8 : RUN chmod 755  . -R
 ---> Using cache
 ---> a1803b721f75
Step 8/8 : EXPOSE 8080
 ---> Running in ceeabf67b57e
Removing intermediate container ceeabf67b57e
 ---> 05713eefd125
Successfully built 05713eefd125
Successfully tagged tomcat:ashuv1

```

## login & push httpd image

```
4502  docker  build  -t  dockerashu/httpd:oraclejan2021v1  . 
❯ docker login  -u dockerashu
Password: 
Login Succeeded
❯ docker push  dockerashu/httpd:oraclejan2021v1
The push refers to repository [docker.io/dockerashu/httpd]
7b3988d1d6e0: Pushed 
143a4ef41fa2: Pushed 
2653d992f4ef: Mounted from library/centos 
oraclejan2021v1: digest: sha256:6d1372a6fbe11d5b5e4089c37ed8077e3b054c76c08f8cb0c5

```

## Networking 

<img src="bridge.png">

## Docker networks 

```
❯ docker network  ls
NETWORK ID     NAME      DRIVER    SCOPE
0d0902ba31e0   bridge    bridge    local
f3976dd88ab6   host      host      local
0e4420a12f63   none      null      local
❯ docker network inspect  0d0902ba31e0
[
    {
        "Name": "bridge",
        "Id": "0d0902ba31e0dbc783d1bf4b530e833b810c798d37dc8e768fcfc950d00ba878",
        "Created": "2021-01-27T03:59:07.647173596Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "172.17.0.0/16",
                    "Gateway": "172.17.0.1"
                }

```

## checking container interface 

```
❯ docker exec -it x1ashu sh
/ # ifconfig 
eth0      Link encap:Ethernet  HWaddr 02:42:AC:11:00:02  
          inet addr:172.17.0.2  Bcast:172.17.255.255  Mask:255.255.0.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:114 errors:0 dropped:0 overruns:0 frame:0
          TX packets:101 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:10560 (10.3 KiB)  TX bytes:9498 (9.2 KiB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
          
          
          
```

## custom bridge creation 

```
 4533  docker network create  ashubr1
 4534  docker network ls
 4535  docker network  inspect  ashubr1
❯ docker run -d --name c1  alpine ping fb.com
7c7e1c0d0feb85ab8ccd9ac800bbe4b145dcb7f6617c5b475aca4398ca0826ee
^Cdocke%                                                                                                                       ❯ docker rm c1 -f
c1
❯ 
❯ docker run -d --name c1 --network ashubr1   alpine ping fb.com
a4b9de6c2aa3a3f59f24750631ce6ab8c76f32a2a5eb42cf47d053b1f10efa19

❯ 
❯ docker run -d --name c2 --network ashubr1   alpine ping fb.com
f93ffc2f56d0f0106985f2561808f4819cd9d11ebfa22f0d6994c858eb75fad2
❯ 
❯ docker exec -it c1 sh
/ # ping c2 
PING c2 (172.18.0.3): 56 data bytes
64 bytes from 172.18.0.3: seq=0 ttl=255 time=0.127 ms
64 bytes from 172.18.0.3: seq=1 ttl=255 time=0.110 ms
64 bytes from 172.18.0.3: seq=2 ttl=255 time=0.113 ms
^C
--- c2 ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 0.110/0.116/0.127 ms

```

## POrt forwarding 

<img src="portf.png">

## docker overlay networking using swarm 

<img src="overlay.png">

# storage in Docker & containers 

<img src="st.png">

## for docker engine creating space 

```
[root@ip-172-31-43-246 ~]# mkfs.xfs   /dev/xvdf 
meta-data=/dev/xvdf              isize=512    agcount=4, agsize=2752512 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=1, sparse=0
data     =                       bsize=4096   blocks=11010048, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
log      =internal log           bsize=4096   blocks=5376, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
[root@ip-172-31-43-246 ~]# 
[root@ip-172-31-43-246 ~]# mkdir   /mnt/oracle
[root@ip-172-31-43-246 ~]# mount  /dev/xvdf  /mnt/oracle/
[root@ip-172-31-43-246 ~]# vim   /etc/fstab 
[root@ip-172-31-43-246 ~]# mount -a

```

## configuring docker engine 

```
[root@ip-172-31-43-246 ~]# cat  /etc/sysconfig/docker
# The max number of open files for the daemon itself, and all
# running containers.  The default value of 1048576 mirrors the value
# used by the systemd service unit.
DAEMON_MAXFILES=1048576

# Additional startup options for the Docker daemon, for example:
# OPTIONS="--ip-forward=true --iptables=true"
# By default we limit the number of open files per container
OPTIONS="--default-ulimit nofile=1024:4096  -H tcp://0.0.0.0:2375  -g  /mnt/oracle"

# How many seconds the sysvinit script waits for the pidfile to appear
# when starting the daemon.
DAEMON_PIDFILE_TIMEOUT=10

```


## loading services 

```
[root@ip-172-31-43-246 ~]# systemctl daemon-reload 
[root@ip-172-31-43-246 ~]# systemctl restart docker

```

## checking it 

```
❯ docker  info
Client:
 Context:    ashuaws
 Debug Mode: false
 Plugins:
  app: Docker App (Docker Inc., v0.9.1-beta3)
  buildx: Build with BuildKit (Docker Inc., v0.5.1-docker)
  scan: Docker Scan (Docker Inc., v0.5.0)

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 19.03.13-ce
 Storage Driver: overlay2
  Backing Filesystem: xfs
  Supports d_type: true
  Native Overlay Diff: true
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: c623d1b36f09f8ef6536a057bd658b3aa8632828
 runc version: ff819c7e9184c13b7c2607fe6c30ae19403a7aff
 init version: de40ad0 (expected: fec3683)
 Security Options:
  seccomp
   Profile: default
 Kernel Version: 4.14.209-160.339.amzn2.x86_64
 Operating System: Amazon Linux 2
 OSType: linux
 Architecture: x86_64
 CPUs: 2
 Total Memory: 3.85GiB
 Name: ip-172-31-43-246.ec2.internal
 ID: 4MIK:ZUZD:J3FL:SBMM:YOIK:Y4YP:RIPI:6VFS:4IG5:F2MS:2NBY:E6DH
 Docker Root Dir: /mnt/oracle

```


## restoring old location data to new location 

```
 13  rsync -avp  /var/lib/docker/  /mnt/oracle/
   14  systemctl restart docker 
   
```

