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

```

### Deployment 

```

```



