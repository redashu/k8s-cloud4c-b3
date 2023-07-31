# k8s-cloud4c-b3

### Deploy a two tier web app Db and WEb ui 

<img src="deploy1.png">

### creating mysql deployment manifest 

```
kubectl  create  deployment ashu-db --image=mysql:8.0  --port=3306 --dry-run=client  -o yaml  >mysql_deploy.yaml
```

### creating secret to store db admin password 

```
[ashu@ip-172-31-5-47 day11-two-tierapp]$ kubectl  create  secret   generic  ashudb-root-pass  --from-
--from-env-file  (Specify the path to a file to read lines of key=val pairs to create a secret.)
--from-file      (Key files can be specified using their file path, in which case a default name will be given to them, …)
--from-literal   (Specify a key and literal value to insert in secret (i.e. mykey=somevalue))

========> 

[ashu@ip-172-31-5-47 day11-two-tierapp]$ kubectl  create  secret   generic  ashudb-root-pass  --from-literal  mydbpass="Db@12345" --dry-run=client -o yaml  >secret_root.yaml 

```

### using secret in deployment file 

```

```

