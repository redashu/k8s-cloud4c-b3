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

```

