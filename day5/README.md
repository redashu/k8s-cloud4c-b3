# k8s-cloud4c-b3

### Revision 

<img src="rev.png">

### Redeploy same pod manifest of last day 

```
[ashu@ip-172-31-5-47 ashu-docker-images]$ ls
java-app  k8s-manifests  labs.txt  node-app  python-app  webui-app
[ashu@ip-172-31-5-47 ashu-docker-images]$ cd  k8s-manifests/
[ashu@ip-172-31-5-47 k8s-manifests]$ ls
ashupod1.yaml
[ashu@ip-172-31-5-47 k8s-manifests]$ kubectl  create -f  ashupod1.yaml 
pod/ashu-node-pod1 created
[ashu@ip-172-31-5-47 k8s-manifests]$ kubectl  get  pods
NAME             READY   STATUS    RESTARTS   AGE
ashu-node-pod1   1/1     Running   0          7s
dasa-node-pod1   1/1     Running   0          4m5s
[ashu@ip-172-31-5-47 k8s-manifests]$ 
```

## master node -- schedular component 

<img src="sch.png">

### checking pod node status

```
[ashu@ip-172-31-5-47 k8s-manifests]$ kubectl   get  nodes
NAME         STATUS   ROLES           AGE   VERSION
masternode   Ready    control-plane   43h   v1.27.3
node1        Ready    <none>          43h   v1.27.3
node2        Ready    <none>          43h   v1.27.3
node3        Ready    <none>          43h   v1.27.3
[ashu@ip-172-31-5-47 k8s-manifests]$ kubectl  get  pods  ashu-node-pod1  -o wide
NAME             READY   STATUS    RESTARTS   AGE   IP               NODE    NOMINATED NODE   READINESS GATES
ashu-node-pod1   1/1     Running   0          18m   192.168.104.22   node2   <none>           <none>
[ashu@ip-172-31-5-47 k8s-manifests]$ 

```



