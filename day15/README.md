# k8s-cloud4c-b3

## enable auto completion in kubectl on bash shell

```
source <(kubectl completion bash)

echo "source <(kubectl completion bash)" >> ~/.bashrc
```

### Helm introduction 

<img src="helm.png">

### Overall helm 

<img src="helm1.png">

## First step to add repo url 

```
[ashu@ip-172-31-5-47 ashu-docker-images]$ helm repo ls
NAME                    URL                                               
prometheus-community    https://prometheus-community.github.io/helm-charts
ashu-repo1              https://charts.helm.sh/stable                     
[ashu@ip-172-31-5-47 ashu-docker-images]$ 
[ashu@ip-172-31-5-47 ashu-docker-images]$ 
[ashu@ip-172-31-5-47 ashu-docker-images]$ helm repo add ashu-repo2 https://charts.bitnami.com/bitnami
"ashu-repo2" has been added to your repositories
[ashu@ip-172-31-5-47 ashu-docker-images]$ 
[ashu@ip-172-31-5-47 ashu-docker-images]$ 
[ashu@ip-172-31-5-47 ashu-docker-images]$ helm repo ls
NAME                    URL                                               
prometheus-community    https://prometheus-community.github.io/helm-charts
ashu-repo1              https://charts.helm.sh/stable                     
ashu-repo2              https://charts.bitnami.com/bitnami                
[ashu@ip-172-31-5-47 ashu-docker-images]$ 

```

### searching packages in helm 

```
[ashu@ip-172-31-5-47 ashu-docker-images]$ helm search repo  nginx 
NAME                                            CHART VERSION   APP VERSION     DESCRIPTION                                       
ashu-repo1/nginx-ingress                        1.41.3          v0.34.1         DEPRECATED! An nginx Ingress controller that us...
ashu-repo1/nginx-ldapauth-proxy                 0.1.6           1.13.5          DEPRECATED - nginx proxy with ldapauth            
ashu-repo1/nginx-lego                           0.3.1                           Chart for nginx-ingress-controller and kube-lego  
ashu-repo2/nginx                                15.1.2          1.25.1          NGINX Open Source is a web server that can be a...
ashu-repo2/nginx-ingress-controller             9.7.7           1.8.1           NGINX Ingress Controller is an Ingress controll...
ashu-repo2/nginx-intel                          2.1.15          0.4.9           DEPRECATED NGINX Open Source for Intel is a lig...
prometheus-community/prometheus-nginx-exporter  0.1.1           0.11.0          A Helm chart for the Prometheus NGINX Exporter    
ashu-repo1/gcloud-endpoints                     0.1.2           1               DEPRECATED Develop, deploy, protect and monitor...
[ashu@ip-172-31-5-47 ashu-docker-images]$ 

```

### deploy package in k8s 

```
[ashu@ip-172-31-5-47 ashu-docker-images]$ helm install  ashu-webapp   ashu-repo2/nginx 
NAME: ashu-webapp
LAST DEPLOYED: Fri Aug  4 04:18:58 2023
NAMESPACE: ashu-apps
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
CHART NAME: nginx
CHART VERSION: 15.1.2
APP VERSION: 1.25.1

```

### verify deploy status

```
[ashu@ip-172-31-5-47 ashu-docker-images]$ helm  ls
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
ashu-webapp     ashu-apps       1               2023-08-04 04:18:58.794325343 +0000 UTC deployed        nginx-15.1.2    1.25.1     
[ashu@ip-172-31-5-47 ashu-docker-images]$ 
```

### uninstall -- deleting 

```
ashu@ip-172-31-5-47 ashu-docker-images]$ helm ls
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
ashu-webapp     ashu-apps       1               2023-08-04 04:18:58.794325343 +0000 UTC deployed        nginx-15.1.2    1.25.1     
[ashu@ip-172-31-5-47 ashu-docker-images]$ 
[ashu@ip-172-31-5-47 ashu-docker-images]$ 
[ashu@ip-172-31-5-47 ashu-docker-images]$ helm uninstall  ashu-webapp
release "ashu-webapp" uninstalled
[ashu@ip-172-31-5-47 ashu-docker-images]$ 
[ashu@ip-172-31-5-47 ashu-docker-images]$ helm ls
NAME    NAMESPACE       REVISION        UPDATED STATUS  CHART   APP VERSION
[ashu@ip-172-31-5-47 ashu-docker-images]$ 
[ashu@ip-172-31-5-47 ashu-docker-images]$ 
[ashu@ip-172-31-5-47 ashu-docker-images]$ kubectl  get  all
No resources found in ashu-apps namespace.
[ashu@ip-172-31-5-47 ashu-docker-images]$ 

```


