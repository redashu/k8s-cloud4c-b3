# k8s-cloud4c-b3

### Revision 

##  Creating Dockerfile with sample UI application to build docker image 

### creating a new project directory 
```
[ashu@ip-172-31-5-47 ashu-docker-images]$ mkdir new-webapp
[ashu@ip-172-31-5-47 ashu-docker-images]$ cd new-webapp/
[ashu@ip-172-31-5-47 new-webapp]$ git clone https://github.com/schoolofdevops/html-sample-app.git
Cloning into 'html-sample-app'...
remote: Enumerating objects: 74, done.
remote: Counting objects: 100% (74/74), done.
remote: Compressing objects: 100% (69/69), done.
remote: Total 74 (delta 5), reused 72 (delta 5), pack-reused 0
Receiving objects: 100% (74/74), 1.38 MiB | 3.08 MiB/s, done.
Resolving deltas: 100% (5/5), done.
[ashu@ip-172-31-5-47 new-webapp]$ ls
html-sample-app
[ashu@ip-172-31-5-47 new-webapp]$ 
```

### Dockerfile and .dockerignore adding to the source code

```
html-sample-app/.git
html-sample-app/*.txt
```

### 

```
FROM nginx
LABEL name=ashutoshh
COPY html-sample-app /usr/share/nginx/html/
```

### lets build image  and push image to docker hub 

```
[ashu@ip-172-31-5-47 new-webapp]$ ls
Dockerfile  html-sample-app
[ashu@ip-172-31-5-47 new-webapp]$ 
[ashu@ip-172-31-5-47 new-webapp]$ docker build -t  docker.io/dockerashu/ashu-app:uiv1 . 
Sending build context to Docker daemon  2.099MB
Step 1/3 : FROM nginx
 ---> 021283c8eb95
Step 2/3 : LABEL name=ashutoshh
 ---> Using cache
 ---> d6bf21fa45a3
Step 3/3 : COPY html-sample-app /usr/share/nginx/html/
 ---> 49e6fb96c8eb
Successfully built 49e6fb96c8eb
Successfully tagged dockerashu/ashu-app:uiv1


[ashu@ip-172-31-5-47 new-webapp]$ docker login 
Authenticating with existing credentials...
WARNING! Your password will be stored unencrypted in /home/ashu/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded


[ashu@ip-172-31-5-47 new-webapp]$ docker push docker.io/dockerashu/ashu-app:uiv1
The push refers to repository [docker.io/dockerashu/ashu-app]
23cc067ff78e: Pushed 
3c9d04c9ebd5: Layer already exists 
434c6a715c30: Layer already exists 
9fdfd12bc85b: Layer already exists 
f36897eea34d: Layer already exists 
```
