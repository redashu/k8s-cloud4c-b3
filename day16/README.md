# k8s-cloud4c-b3

## COntainer are having ephemral nature by default 

<img src="em.png">

### storage in k8s 

<img src="st1.png">

### volume vs PV 

<img src="vold.png">

### Creating mysql deployment without volume 

## manifests

### configmap 

```
kubectl create configmap ashu-db-cm  --from-env-file  db-details.env --dry-run=client -o yaml >cm.yaml

===db-details.env===

MYSQL_DATABASE=ashucloud4cdb

===========>
ashu@ip-172-31-5-47 day16]$ kubectl  create -f cm.yaml 
configmap/ashu-db-cm created
[ashu@ip-172-31-5-47 day16]$ kubectl  get cm
NAME               DATA   AGE
ashu-db-cm         1      3s
kube-root-ca.crt   1      2d23h
```

### secret 

```
==< db-cred.env == >
MYSQL_ROOT_PASSWORD=RootdbPass@123
MYSQL_USER=ashu
MYSQL_PASSWORD=Ashudb@098

====>>
[ashu@ip-172-31-5-47 day16]$ ls
cm.yaml  db-cred.env  db-details.env

[ashu@ip-172-31-5-47 day16]$ kubectl  create secret 
docker-registry  (Create a secret for use with a Docker registry)
generic          (Create a secret from a local file, directory, or literal value)
tls              (Create a TLS secret)

[ashu@ip-172-31-5-47 day16]$ kubectl  create secret generic  ashu-db-cred  --from-env-file  db-cred.env --dry-run=client -o yaml  >secret.yaml 
[ashu@ip-172-31-5-47 day16]$ kubectl  create -f secret.yaml 
secret/ashu-db-cred created

[ashu@ip-172-31-5-47 day16]$ kubectl  get  secrets 
NAME           TYPE     DATA   AGE
ashu-db-cred   Opaque   3      3s
[ashu@ip-172-31-5-47 day16]$ 


```

### Deployment 

```

```



