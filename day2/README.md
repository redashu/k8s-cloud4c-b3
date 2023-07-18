# k8s-cloud4c-b3

### understanding app containerization process

<img src="appc.png">

### creating directory structure to store the source code

```
ashu@ip-172-31-5-47 ~]$ whoami
ashu
[ashu@ip-172-31-5-47 ~]$ ls
[ashu@ip-172-31-5-47 ~]$ mkdir  ashu-docker-images
[ashu@ip-172-31-5-47 ~]$ 
[ashu@ip-172-31-5-47 ~]$ mkdir  ashu-docker-images/node-app
[ashu@ip-172-31-5-47 ~]$ mkdir  ashu-docker-images/java-app
[ashu@ip-172-31-5-47 ~]$ mkdir  ashu-docker-images/python-app
[ashu@ip-172-31-5-47 ~]$ mkdir  ashu-docker-images/webui-app
[ashu@ip-172-31-5-47 ~]$ ls
ashu-docker-images
[ashu@ip-172-31-5-47 ~]$ ls ashu-docker-images/
java-app  node-app  python-app  webui-app
[ashu@ip-172-31-5-47 ~]$ 
```

### taking some sample webui code to convert / build into docker image

```
[ashu@ip-172-31-5-47 ashu-docker-images]$ ls
java-app  node-app  python-app  webui-app
[ashu@ip-172-31-5-47 ashu-docker-images]$ cd  webui-app/
[ashu@ip-172-31-5-47 webui-app]$ ls
[ashu@ip-172-31-5-47 webui-app]$ git clone https://github.com/schoolofdevops/html-sample-app.git
Cloning into 'html-sample-app'...
remote: Enumerating objects: 74, done.
remote: Counting objects: 100% (74/74), done.
remote: Compressing objects: 100% (69/69), done.
remote: Total 74 (delta 5), reused 72 (delta 5), pack-reused 0
Receiving objects: 100% (74/74), 1.38 MiB | 19.37 MiB/s, done.
Resolving deltas: 100% (5/5), done.
[ashu@ip-172-31-5-47 webui-app]$ ls
html-sample-app
[ashu@ip-172-31-5-47 webui-app]$ ls html-sample-app/
assets  elements.html  generic.html  html5up-phantom.zip  images  index.html  LICENSE.txt  README.txt
[ashu@ip-172-31-5-47 webui-app]$ 
```

### creating Dockerfile for html code base

## Dockerfile

```
FROM nginx
# this mean we are refering nginx lib from Docker hub
LABEL name=ashutoshh
LABEL email=ashutoshh@linux.com
# optional info but good to write if someone need to contact
COPY html-sample-app /usr/share/nginx/html/
# we are coping html-code to the location of nginx 
# from where nginx can read by default 

```

### lets build image of webui app using docker build

```
[ashu@ip-172-31-5-47 webui-app]$ ls
Dockerfile  html-sample-app

====
[ashu@ip-172-31-5-47 webui-app]$ docker build -t ashu-ui:v1 . 
Sending build context to Docker daemon  3.629MB
Step 1/4 : FROM nginx
latest: Pulling from library/nginx
faef57eae888: Pull complete 
76579e9ed380: Pull complete 
cf707e233955: Pull complete 
91bb7937700d: Pull complete 
4b962717ba55: Pull complete 
f46d7b05649a: Pull complete 
103501419a0a: Pull complete 
Digest: sha256:08bc36ad52474e528cc1ea3426b5e3f4bad8a130318e3140d6cfe29c8892c7ef
Status: Image is up to date for nginx:latest
 ---> 021283c8eb95
Step 2/4 : LABEL name=ashutoshh
 ---> Running in 7ae5df958edb
Removing intermediate container 7ae5df958edb
 ---> d6bf21fa45a3
Step 3/4 : LABEL email=ashutoshh@linux.com
 ---> Running in 5a23ea2c00a7
Removing intermediate container 5a23ea2c00a7
 ---> 43cc818e30ac
Step 4/4 : COPY html-sample-app /usr/share/nginx/html/
 ---> 30bb75b24fc6
Successfully built 30bb75b24fc6
Successfully tagged ashu-ui:v1
```

### verify build 

```
[ashu@ip-172-31-5-47 webui-app]$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED              SIZE
nikita-ui    v1        6c0c0f181589   37 seconds ago       190MB
ashu-ui      v1        30bb75b24fc6   About a minute ago   190MB
ankita-ui    v1        b69e948143eb   About a minute ago   190MB
vital-ui     v1        bdf3530b9f02   About a minute ago   190MB
nginx        latest    021283c8eb95   13 days ago          187MB
```

### creating and verify container status

```
======> creating container
 docker run --name  ashu-ui-app  -d  ashu-ui:v1  
821f9559ca3c4e8aef5f25f9c9c2be7a732a3e53ab2cddc497850b4a5e2fb8bf

=======> verify container listing 
 docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS     NAMES
bf562b318b56   vital-ui:v1    "/docker-entrypoint.…"   3 seconds ago   Up 2 seconds   80/tcp    vital-ui-app
09e225b1c8f2   nikita-ui:v1   "/docker-entrypoint.…"   3 seconds ago   Up 2 seconds   80/tcp    nikita-ui-app
7285f7214b4a   rasi-ui:v1     "/docker-entrypoint.…"   3 seconds ago   Up 2 seconds   80/tcp    rasi-ui-app
aad60501bee3   ankita-ui:v1   "/docker-entrypoint.…"   4 seconds ago   Up 3 seconds   80/tcp    ankita-ui-app
821f9559ca3c   ashu-ui:v1     "/docker-entrypoint.…"   7 seconds ago   Up 6 seconds   80/tcp    ashu-ui-app
[ashu@ip-172-31-5-47 webui-app]$ 
```

### manually stop and remove container

```
=====> stopping container

[ashu@ip-172-31-5-47 webui-app]$ docker  kill  ashu-ui-app 
ashu-ui-app

=====> removing container 
[ashu@ip-172-31-5-47 webui-app]$ docker rm ashu-ui-app
ashu-ui-app
[ashu@ip-172-31-5-47 webui-app]$ 
```

### what if we only kill not remove

```
[ashu@ip-172-31-5-47 webui-app]$ docker ps
CONTAINER ID   IMAGE                COMMAND                  CREATED              STATUS              PORTS     NAMES
b82024a9ce79   girish:v1            "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp    girish-ui-app
e6992ec444ac   ashu-ui:v1           "/docker-entrypoint.…"   6 minutes ago        Up 6 minutes        80/tcp    ashuc1
ef514a55f0b6   chandrshekar-ui:v1   "/docker-entrypoint.…"   11 minutes ago       Up 11 minutes       80/tcp    chandrashekar-ui-app
[ashu@ip-172-31-5-47 webui-app]$ docker kill ashuc1
ashuc1
[ashu@ip-172-31-5-47 webui-app]$ docker ps
CONTAINER ID   IMAGE                COMMAND                  CREATED              STATUS              PORTS     NAMES
b82024a9ce79   girish:v1            "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp    girish-ui-app
ef514a55f0b6   chandrshekar-ui:v1   "/docker-entrypoint.…"   11 minutes ago       Up 11 minutes       80/tcp    chandrashekar-ui-app
[ashu@ip-172-31-5-47 webui-app]$ docker ps -a
CONTAINER ID   IMAGE                COMMAND                  CREATED              STATUS                            PORTS     NAMES
b82024a9ce79   girish:v1            "/docker-entrypoint.…"   About a minute ago   Up About a minute                 80/tcp    girish-ui-app
e6992ec444ac   ashu-ui:v1           "/docker-entrypoint.…"   6 minutes ago        Exited (137) 7 seconds ago                  ashuc1
ef514a55f0b6   chandrshekar-ui:v1   "/docker-entrypoint.…"   11 minutes ago       Up 11 minutes                     80/tcp    chandrashekar-ui-app
73cd9ee2be0f   dasharath-ui:v1      "/docker-entrypoint.…"   11 minutes ago       Exited (137) 2 minutes ago                  webui-app
911bcefd5c5d   siva-ui:v1           "/docker-entrypoint.…"   14 minutes ago       Exited (137) About a minute ago             siva-ui-app
[ashu@ip-172-31-5-47 webui-app]$ docker start  ashuc1
ashuc1
[ashu@ip-172-31-5-47 webui-app]$ docker  ps
CONTAINER ID   IMAGE                COMMAND                  CREATED              STATUS              PORTS     NAMES
b82024a9ce79   girish:v1            "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp    girish-ui-app
e6992ec444ac   ashu-ui:v1           "/docker-entrypoint.…"   6 minutes ago        Up 2 seconds        80/tcp    ashuc1
ef514a55f0b6   chandrshekar-ui:v1   "/docker-entrypoint.…"   11 minutes ago       Up 11 minutes       80/tcp    chandrashekar-ui-app
[ashu@ip-172-31-5-47 webui-app]$ 
```

## PYthon code to docker image

### hello.py 

```
import time
while 3 > 2 :
    print("Hello cloud4c team  !!")
    time.sleep(2)
    print("Welcome to Docker ")
    time.sleep(1)
    print("Tomorrow will start with kubernetes ..")
    print("_______________")
    time.sleep(1)
```

### Dockerfile

```
FROM python:3.9
LABEL email=ashutoshh@linux.com
RUN mkdir /ashucode 
# created a folder inside new docker image
COPY hello.py  /ashucode/hello.py 
# we have to let our container know how to run python code
CMD ["python","/ashucode/hello.py"]
# cmd will be automatically executed once you create container by docker run

```

### lets build image

```
[ashu@ip-172-31-5-47 webui-app]$ ls
Dockerfile  html-sample-app
[ashu@ip-172-31-5-47 webui-app]$ cd ..
[ashu@ip-172-31-5-47 ashu-docker-images]$ ls
java-app  node-app  python-app  webui-app
[ashu@ip-172-31-5-47 ashu-docker-images]$ cd python-app/
[ashu@ip-172-31-5-47 python-app]$ ls
Dockerfile  hello.py
[ashu@ip-172-31-5-47 python-app]$ docker build -t ashupy:v11 . 
Sending build context to Docker daemon  3.072kB
Step 1/5 : FROM python:3.9
3.9: Pulling from library/python
d52e4f012db1: Already exists 
7dd206bea61f: Already exists 
2320f9be4a9c: Already exists 
6e5565e0ba8d: Already exists 
d3797e13cc41: Already exists 
9421d62bef94: Pull complete 
19d7d75bfdca: Pull complete 
67f28346abde: Pull complete 
Digest: sha256:ba10a2af9d6c3bd0d20c46ecbf866dabcbad4e6a3dd7b82e2dfb1a9b6d479d87
Status: Downloaded newer image for python:3.9
 ---> 1d7821476b67
Step 2/5 : LABEL email=ashutoshh@linux.com
 ---> Running in 2c8b66422a15
Removing intermediate container 2c8b66422a15
 ---> aa3cd5e756ed
Step 3/5 : RUN mkdir /ashucode
 ---> Running in 83eca7ffe0dc
Removing intermediate container 83eca7ffe0dc
 ---> cb6324484c87
Step 4/5 : COPY hello.py  /ashucode/hello.py
 ---> 3c97c59cfbf8
Step 5/5 : CMD ["python","/ashucode/hello.py"]
 ---> Running in efc6db20f330
Removing intermediate container efc6db20f330
 ---> da6173f10096
Successfully built da6173f10096
Successfully tagged ashupy:v11
```

### verify 

```
[ashu@ip-172-31-5-47 python-app]$ docker images  | grep ashu
ashupy             v11       da6173f10096   About a minute ago   997MB
ashu-ui            v1        277fb6dca6b5   38 minutes ago       190MB
[ashu@ip-172-31-5-47 python-app]$ 

```

### create contaienr and check output

```
[ashu@ip-172-31-5-47 python-app]$ docker run --name ashupyc1  -d  -it ashupy:v11 
5bcc3eb1e2924c5568919e8e3b9ad44662ea7f138b952d9cad01ecab64ce855e
[ashu@ip-172-31-5-47 python-app]$ docker ps
CONTAINER ID   IMAGE            COMMAND                  CREATED         STATUS                  PORTS     NAMES
784c5f3ffadc   ankitapy:v11     "python /ankitacode/…"   1 second ago    Up Less than a second             ankitapyc1
5bcc3eb1e292   ashupy:v11       "python /ashucode/he…"   3 seconds ago   Up 2 seconds                      ashupyc1
28cd8aed7a4c   siva-python:v1   "python /sivapythonc…"   3 minutes ago   Up 3 minutes                      siva-python-app



[ashu@ip-172-31-5-47 python-app]$ docker  logs  ashupyc1
Hello cloud4c team  !!
Welcome to Docker 
Tomorrow will start with kubernetes ..
_______________
```


