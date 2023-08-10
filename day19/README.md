# k8s-cloud4c-b3

### targets

<img src="tg.png">

### Understanding CRD in k8s

<img src="crd.png">

### Quick revision of HeLM 

<img src="helm.png">

### Helm charts 

<img src="helm1.png">

### revision of basics

```
 1009  helm  search repo   nginx 
 1010  helm install  ashu-webapp  ashu-repo2/nginx 
 1011  history 
[ashu@ip-172-31-5-47 ashu-docker-images]$ helm ls
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
ashu-webapp     ashu-apps       1               2023-08-10 04:20:32.585060314 +0000 UTC deployed        nginx-15.1.2    1.25.1     
[ashu@ip-172-31-5-47 ashu-docker-images]$ 
[ashu@ip-172-31-5-47 ashu-docker-images]$ 
[ashu@ip-172-31-5-47 ashu-docker-images]$ kubectl  get  deploy
NAME                READY   UP-TO-DATE   AVAILABLE   AGE
ashu-webapp-nginx   1/1     1            1           17s
[ashu@ip-172-31-5-47 ashu-docker-images]$ kubectl  get  svc
NAME                TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
ashu-webapp-nginx   LoadBalancer   10.101.188.161   <pending>     80:30057/TCP   20s
[ashu@ip-172-31-5-47 ashu-docker-images]$ kubectl  get  po
NAME                                 READY   STATUS    RESTARTS   AGE
ashu-webapp-nginx-689f5c8fc7-ttbx2   1/1     Running   0          23s

====>

ashu@ip-172-31-5-47 ashu-docker-images]$ helm ls
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
ashu-webapp     ashu-apps       1               2023-08-10 04:20:32.585060314 +0000 UTC deployed        nginx-15.1.2    1.25.1     
[ashu@ip-172-31-5-47 ashu-docker-images]$ helm uninstall ashu-webapp
release "ashu-webapp" uninstalled
[ashu@ip-172-31-5-47 ashu-docker-images]$ 
[ashu@ip-172-31-5-47 ashu-docker-images]$ 
[ashu@ip-172-31-5-47 ashu-docker-images]$ helm ls
NAME    NAMESPACE       REVISION        UPDATED STATUS  CHART   APP VERSION
[ashu@ip-172-31-5-47 ashu-docker-images]$ 
[ashu@ip-172-31-5-47 ashu-docker-images]$ kubectl  get all
No resources found in ashu-apps namespace.
[ashu@ip-172-31-5-47 ashu-docker-images]$ 



```

### Understanding helm charts

### pulling existing chart

```
[ashu@ip-172-31-5-47 helm-project]$ helm pull ashu-repo2/nginx 
[ashu@ip-172-31-5-47 helm-project]$ ls
nginx-15.1.2.tgz
[ashu@ip-172-31-5-47 h
```

### Decompression of charts package

```
[ashu@ip-172-31-5-47 helm-project]$ ls
nginx-15.1.2.tgz
[ashu@ip-172-31-5-47 helm-project]$ tar xvzf nginx-15.1.2.tgz 
nginx/Chart.yaml
nginx/Chart.lock
nginx/values.yaml
nginx/values.schema.json
nginx/templates/NOTES.txt
nginx/templates/_helpers.tpl
```

### charts is just a organized directory 

```
[ashu@ip-172-31-5-47 helm-project]$ cd  nginx/
[ashu@ip-172-31-5-47 nginx]$ ls
Chart.lock  charts  Chart.yaml  README.md  templates  values.schema.json  values.yaml
[ashu@ip-172-31-5-47 nginx]$ 


```

### using custom values.yaml file to update the existing charts values while install

```
ashu@ip-172-31-5-47 helm-project]$ helm install ashu-app ashu-repo2/nginx    --values  values.yaml 
NAME: ashu-app
LAST DEPLOYED: Thu Aug 10 04:43:31 2023
NAMESPACE: ashu-apps
STATUS: deployed
REVISION: 1
TEST SUITE: None

====>

```


