# k8s-cloud4c-b3

### connect

```
[ashu@ip-172-31-5-47 ashu-docker-images]$ kubectl  config  get-contexts 
CURRENT   NAME                          CLUSTER      AUTHINFO           NAMESPACE
*         kubernetes-admin@kubernetes   kubernetes   kubernetes-admin   ashu-apps
[ashu@ip-172-31-5-47 ashu-docker-images]$ kubectl  delete all --all
pod "ashupod1" deleted
[ashu@ip-172-31-5-47 ashu-docker-images]$ 

```



### understanding apiserver logical desing 

<img src="log.png">

### listing all api-resource in currently running k8s version 

```
[ashu@ip-172-31-5-47 ashu-docker-images]$ kubectl  api-resources 
NAME                              SHORTNAMES   APIVERSION                             NAMESPACED   KIND
bindings                                       v1                                     true         Binding
componentstatuses                 cs           v1                                     false        ComponentStatus
configmaps                        cm           v1                                     true         ConfigMap
endpoints                         ep           v1                                     true         Endpoints
events                            ev           v1                                     true         Event
```

### creating pod using deployment controller 

```
kubectl   create  deployment  ashu-node-deploy  --image=dockerashu/ashunode:version1  --port 3000 --dry-run=client -o yaml >deployment.yaml 
```

### yaml file 

```
apiVersion: apps/v1 # apiversion 
kind: Deployment # resource is deployment controller
metadata:
  creationTimestamp: null
  labels: # label 
    app: ashu-node-deploy
  name: ashu-node-deploy # name of deployment 
  namespace: ashu-apps # namespace info we can write here 
spec:
  replicas: 1 # number of pod we want 
  selector:
    matchLabels:
      app: ashu-node-deploy
  strategy: {}
  template: # for creating pods 
    metadata:
      creationTimestamp: null
      labels: # label of my pods 
        app: ashu-node-deploy # app as key & ashu-node-deploy as value 
    spec:
      containers:
      - image: dockerashu/ashunode:version1
        name: ashunode
        ports:
        - containerPort: 3000
        resources: {}
status: {}

```

### creating deployment controller 

```
[ashu@ip-172-31-5-47 k8s-manifests]$ kubectl   create -f deployment.yaml 
deployment.apps/ashu-node-deploy created

[ashu@ip-172-31-5-47 k8s-manifests]$ kubectl   get  deployment 
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
ashu-node-deploy   1/1     1            1           5s

[ashu@ip-172-31-5-47 k8s-manifests]$ kubectl   get  pods
NAME                                READY   STATUS    RESTARTS   AGE
ashu-node-deploy-5f6dbfdd46-5z8bg   1/1     Running   0          12s

[ashu@ip-172-31-5-47 k8s-manifests]$ kubectl   get  pods -o wide
NAME                                READY   STATUS    RESTARTS   AGE   IP               NODE    NOMINATED NODE   READINESS GATES
ashu-node-deploy-5f6dbfdd46-5z8bg   1/1     Running   0          15s   192.168.135.27   node3   <none>           <none>

[ashu@ip-172-31-5-47 k8s-manifests]$ kubectl   get  pods --show-labels 
NAME                                READY   STATUS    RESTARTS   AGE   LABELS
ashu-node-deploy-5f6dbfdd46-5z8bg   1/1     Running   0          22s   app=ashu-node-deploy,pod-template-hash=5f6dbfdd46
[ashu@ip-172-31-5-47 k8s-manifests]$ 
```
