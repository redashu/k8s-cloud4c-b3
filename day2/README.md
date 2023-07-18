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

