# k8s-cloud4c-b3

### Cross check things

```
[ashu@ip-172-31-5-47 ashu-docker-images]$ kubectl  config get-contexts 
CURRENT   NAME                          CLUSTER      AUTHINFO           NAMESPACE
*         kubernetes-admin@kubernetes   kubernetes   kubernetes-admin   ashu-apps

[ashu@ip-172-31-5-47 ashu-docker-images]$ kubectl  get deploy
NAME      READY   UP-TO-DATE   AVAILABLE   AGE
ashu-db   1/1     1            1           23h

[ashu@ip-172-31-5-47 ashu-docker-images]$ 
[ashu@ip-172-31-5-47 ashu-docker-images]$ kubectl  get po
NAME                       READY   STATUS    RESTARTS        AGE
ashu-db-77b6d86d6f-86ffd   1/1     Running   2 (7m14s ago)   22h

[ashu@ip-172-31-5-47 ashu-docker-images]$ 
[ashu@ip-172-31-5-47 ashu-docker-images]$ kubectl  get po -o wide
NAME                       READY   STATUS    RESTARTS        AGE   IP              NODE    NOMINATED NODE   READINESS GATES
ashu-db-77b6d86d6f-86ffd   1/1     Running   2 (7m18s ago)   22h   192.168.135.9   node3   <none>           <none>

[ashu@ip-172-31-5-47 ashu-docker-images]$ 
[ashu@ip-172-31-5-47 ashu-docker-images]$ kubectl  get  svc
NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
db-lb-ashu   ClusterIP   10.102.140.206   <none>        3306/TCP   22h

[ashu@ip-172-31-5-47 ashu-docker-images]$ 
[ashu@ip-172-31-5-47 ashu-docker-images]$ kubectl  get  ep 
NAME         ENDPOINTS            AGE
db-lb-ashu   192.168.135.9:3306   22h

[ashu@ip-172-31-5-47 ashu-docker-images]$ kubectl  get  secret
NAME               TYPE     DATA   AGE
ashudb-root-pass   Opaque   1      23h
ashudb-user-pass   Opaque   2      22h
[ashu@ip-172-31-5-47 ashu-docker-images]$ 
```
