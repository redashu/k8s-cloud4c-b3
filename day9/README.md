# k8s-cloud4c-b3

### k8s hidden part 1 

### all the component is running under kube-system namespaces

```
[ashu@ip-172-31-5-47 ashu-docker-images]$ kubectl   get  ns  | grep kube
kube-node-lease        Active   7d18h
kube-public            Active   7d18h
kube-system            Active   7d18h
kubernetes-dashboard   Active   2d
[ashu@ip-172-31-5-47 ashu-docker-images]$ kubectl   -n kube-system   get  pods 
NAME                                       READY   STATUS    RESTARTS       AGE
calico-kube-controllers-6c99c8747f-r4ghn   1/1     Running   11 (25m ago)   7d19h
calico-node-hm9dh                          1/1     Running   12 (25m ago)   7d19h
calico-node-j76x4                          1/1     Running   12 (25m ago)   7d19h
calico-node-jlvpf                          1/1     Running   12 (25m ago)   7d19h
calico-node-tbj8x                          1/1     Running   12 (25m ago)   7d19h
```

###  Controllers --- 
