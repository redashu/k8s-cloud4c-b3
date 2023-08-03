# k8s-cloud4c-b3

## Simplify k8s 

<img src="k8sall.png">

## Ingress controller again 

### cleaning up all namespace content 

```
kubectl  delete all,cm,secret,ingress --all
```

### creating deployment controller for react app

```
[ashu@ip-172-31-5-47 ashu-docker-images]$ mkdir  ingress-win
[ashu@ip-172-31-5-47 ashu-docker-images]$ cd ingress-win/
[ashu@ip-172-31-5-47 ingress-win]$ ls
[ashu@ip-172-31-5-47 ingress-win]$ kubectl create  deployment  ashu-app --image=dockerashu/reactapp:version1 --port 3000  --dry-run=client -o yaml  >deploy.yaml 
[ashu@ip-172-31-5-47 ingress-win]$ 

```

### deploy manifest

```
[ashu@ip-172-31-5-47 ingress-win]$ kubectl  apply -f  deploy.yaml 
deployment.apps/ashu-app created
[ashu@ip-172-31-5-47 ingress-win]$ kubectl  get  deploy
NAME       READY   UP-TO-DATE   AVAILABLE   AGE
ashu-app   1/1     1            1           8s
[ashu@ip-172-31-5-47 ingress-win]$ kubectl  get po
NAME                       READY   STATUS    RESTARTS   AGE
ashu-app-cbdc6cf79-mgrtg   1/1     Running   0          10s
[ashu@ip-172-31-5-47 ingress-win]$ 
```

### creating Np/LB service to expose app outside k8s cluster

```
[ashu@ip-172-31-5-47 ingress-win]$ kubectl  get  deploy
NAME       READY   UP-TO-DATE   AVAILABLE   AGE
ashu-app   1/1     1            1           3m29s
[ashu@ip-172-31-5-47 ingress-win]$ kubectl  expose deployment ashu-app --type NodePort --port 3000 --name ashulb1 --dry-run=client -o yaml >npsvc.yaml 
[ashu@ip-172-31-5-47 ingress-win]$ kubectl  create -f npsvc.yaml 
service/ashulb1 created
[ashu@ip-172-31-5-47 ingress-win]$ kubectl  get  svc
NAME      TYPE       CLUSTER-IP    EXTERNAL-IP   PORT(S)          AGE
ashulb1   NodePort   10.105.14.5   <none>        3000:32599/TCP   3s
[ashu@ip-172-31-5-47 ingress-win]$ 
```

### Because Ingress controller is bringing traffic to inside k8s cluster so we never have to expose webapp outside 

<img src="cls.png">

