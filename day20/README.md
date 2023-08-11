# k8s-cloud4c-b3

### help 

```
  kubectl create secret docker-registry  my-secret  --docker-server cloud4c.azurecr.io  --docker-username cloud4c   --docker-password="x8YQ/ogHiBUnrNhNzjpOXB77MAmZ0RQVvCiFTcesAY+ACRAdtpmj" --dry-run=client -o yaml >imgsecret.yaml
 1016  ls
 1017  kubectl  create -f imgsecret.yaml 
 1018  kubectl  create secret generic mongo-cred  --from-env-file  dbcred.env --dry-run=client -o yaml >credmon.yaml
 1019  kubectl  create -f credmon.yaml 
 1020  kubectl  get secrets 
 1021  history 
 1022  kubectl  create deployment ashu-db --image=cloud4c.azurecr.io/mongo:dbv1 --port 27017 --dry-run=client -o yaml >deploymentdb.yaml 
 1023  kubectl  get secrets 
 1024  kubectl  create -f deploymentdb.yaml 
 1025  kubectl  get deploy
 1026  kubectl  get pod
 1027  history 
```

### manifest

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
      imagePullSecrets: # to pull image from private registry
      - name: my-secret 
      containers:
      - image: cloud4c.azurecr.io/mongo:dbv1
        name: mongo
        ports:
        - containerPort: 27017
        resources: {}
        envFrom:
        - secretRef:
            name: mongo-cred
status: {}

```

### adding hostPath volume 

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
      volumes:
      - name: ashu-dbvol
        hostPath:
          path: /db/ashu/mongo
          type: DirectoryOrCreate
      imagePullSecrets: # to pull image from private registry
      - name: my-secret 
      containers:
      - image: cloud4c.azurecr.io/mongo:dbv1
        name: mongo
        ports:
        - containerPort: 27017
        resources: {}
        envFrom:
        - secretRef:
            name: mongo-cred
        volumeMounts:
        - name: ashu-dbvol
          mountPath: /data/db/
status: {}

```

### creating svc

```
[ashu@ip-172-31-5-47 mongo-project]$ kubectl  get deploy
NAME      READY   UP-TO-DATE   AVAILABLE   AGE
ashu-db   1/1     1            1           12s
[ashu@ip-172-31-5-47 mongo-project]$ kubectl  expose deployment ashu-db --type ClusterIP --port 27017 --name lbs1 --dry-run=client -o yaml >svcdb.yaml
[ashu@ip-172-31-5-47 mongo-project]$ kubectl  create -f svcdb.yaml 
service/lbs1 created
[ashu@ip-172-31-5-47 mongo-project]$ kubectl  get svc
NAME   TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)     AGE
lbs1   ClusterIP   10.109.71.67   <none>        27017/TCP   2s
[ashu@ip-172-31-5-47 mongo-project]$ 


```
