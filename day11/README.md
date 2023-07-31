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

=======>
[ashu@ip-172-31-5-47 day11-two-tierapp]$ ls
mysql_deploy.yaml  secret_root.yaml

[ashu@ip-172-31-5-47 day11-two-tierapp]$ 
[ashu@ip-172-31-5-47 day11-two-tierapp]$ kubectl  create  -f  secret_root.yaml 
secret/ashudb-root-pass created

[ashu@ip-172-31-5-47 day11-two-tierapp]$ kubectl  get  secret 
NAME               TYPE     DATA   AGE
ashudb-root-pass   Opaque   1      4s
[ashu@ip-172-31-5-47 day11-two-tierapp]$

```

### using secret in deployment file to assign root / admin password of mysql db 

```
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: ashu-db
  name: ashu-db
spec:
  replicas: 1
  selector:
    matchLabels:
      app: ashu-db
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: ashu-db
    spec:
      containers:
      - image: mysql:8.0
        name: mysql
        ports:
        - containerPort: 3306
        resources: {}
        env: # to create / update cred of db 
        - name: MYSQL_ROOT_PASSWORD
          valueFrom: 
            secretKeyRef:
              name: ashudb-root-pass  # name of the secret 
              key: mydbpass 
         
status: {}

```

### creating one more secret to store non admin db credential 

```
kubectl  create secret generic   ashudb-user-pass  --from-literal  MYSQL_USER=ashu --from-literal MYSQL_PASSWORD="Hello@098"  --dry-run=client -o yaml >general-user-pass-secret.yaml 
```

### created secret again 

```
[ashu@ip-172-31-5-47 day11-two-tierapp]$ ls
general-user-pass-secret.yaml  mysql_deploy.yaml  secret_root.yaml

[ashu@ip-172-31-5-47 day11-two-tierapp]$ kubectl  create -f general-user-pass-secret.yaml 
secret/ashudb-user-pass created

[ashu@ip-172-31-5-47 day11-two-tierapp]$ kubectl  get  secrets 
NAME               TYPE     DATA   AGE
ashudb-root-pass   Opaque   1      22m
ashudb-user-pass   Opaque   2      4s
```

### updating manifest 

```
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: ashu-db
  name: ashu-db
spec:
  replicas: 1
  selector:
    matchLabels:
      app: ashu-db
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: ashu-db
    spec:
      containers:
      - image: mysql:8.0
        name: mysql
        ports:
        - containerPort: 3306
        resources: {}
        env: # to create / update cred of db 
        - name: MYSQL_ROOT_PASSWORD
          valueFrom: 
            secretKeyRef:
              name: ashudb-root-pass  # name of the secret 
              key: mydbpass 
        envFrom: # when secret is already having ENV name stored 
        - secretRef:
            name: ashudb-user-pass

        
         
status: {}

```

### deploy again 

```
ashu@ip-172-31-5-47 day11-two-tierapp]$ kubectl  apply -f mysql_deploy.yaml 
Warning: resource deployments/ashu-db is missing the kubectl.kubernetes.io/last-applied-configuration annotation which is required by kubectl apply. kubectl apply should only be used on resources created declaratively by either kubectl create --save-config or kubectl apply. The missing annotation will be patched automatically.
deployment.apps/ashu-db configured

[ashu@ip-172-31-5-47 day11-two-tierapp]$ kubectl   get  po
NAME                       READY   STATUS    RESTARTS   AGE
ashu-db-77b6d86d6f-86ffd   1/1     Running   0          13s
[ashu@ip-172-31-5-47 day11-two-tierapp]$ 
```

### MYSQL deployment final status

```
ashu@ip-172-31-5-47 day11-two-tierapp]$ kubectl  get secrets 
NAME               TYPE     DATA   AGE
ashudb-root-pass   Opaque   1      33m
ashudb-user-pass   Opaque   2      11m

[ashu@ip-172-31-5-47 day11-two-tierapp]$ kubectl  get deploy
NAME      READY   UP-TO-DATE   AVAILABLE   AGE
ashu-db   1/1     1            1           21m

[ashu@ip-172-31-5-47 day11-two-tierapp]$ kubectl  get po
NAME                       READY   STATUS    RESTARTS   AGE
ashu-db-77b6d86d6f-86ffd   1/1     Running   0          112s
[ashu@ip-172-31-5-47 day11-two-tierapp]$ 


```

### verify mysql db container connection 

```
[ashu@ip-172-31-5-47 day11-two-tierapp]$ kubectl  get  pod
NAME                       READY   STATUS    RESTARTS   AGE
ashu-db-77b6d86d6f-86ffd   1/1     Running   0          13m


[ashu@ip-172-31-5-47 day11-two-tierapp]$ kubectl  exec  -it   ashu-db-77b6d86d6f-86ffd  -- bash 
bash-4.4# 
bash-4.4# 
bash-4.4# mysql -u root -p
Enter password:

Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.34 MySQL Community Server - GPL

Copyright (c) 2000, 2023, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.01 sec)

mysql> exit;
Bye


bash-4.4# exit
exit
```


