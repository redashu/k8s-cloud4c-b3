# k8s-cloud4c-b3

### Refer a webapp

<img src="web1.png">

### problem with bare-metal / physical server 

<img src="bare.png">

### testing or running multiple app in same host OS 

<img src="prob1.png">

## problem with virutal machine for developers

<img src="dev.png">

### Introduction to containers 

<img src="cont1.png">

### containers can by created and managed by various platforms 

<img src="cont2.png">

## Docker installation 

<img src="docker_install.png">

## yes to Docker desktop on developer side

<img src="devd.png">

### COnnecting to remote server using ssh 

```
PS C:\Users\humanfirmware> ssh
usage: ssh [-46AaCfGgKkMNnqsTtVvXxYy] [-B bind_interface]
           [-b bind_address] [-c cipher_spec] [-D [bind_address:]port]
           [-E log_file] [-e escape_char] [-F configfile] [-I pkcs11]
           [-i identity_file] [-J [user@]host[:port]] [-L address]
           [-l login_name] [-m mac_spec] [-O ctl_cmd] [-o option] [-p port]
           [-Q query_option] [-R address] [-S ctl_path] [-W host:port]
           [-w local_tun[:remote_tun]] destination [command]
PS C:\Users\humanfirmware>
PS C:\Users\humanfirmware> ssh  ashu@43.205.161.231
The authenticity of host '43.205.161.231 (43.205.161.231)' can't be established.
ED25519 key fingerprint is SHA256:h5t+VKjGTxNKOkGzuYEFxtbts3Ye2zFOQSY8Ik1bly4.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '43.205.161.231' (ED25519) to the list of known hosts.
ashu@43.205.161.231's password:

       __|  __|_  )
       _|  (     /   Amazon Linux 2 AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-2/
[ashu@ip-172-31-5-47 ~]$ whoami
ashu
[ashu@ip-172-31-5-47 ~]$ uname -r
5.10.184-175.731.amzn2.x86_64
[ashu@ip-172-31-5-47 ~]$
```

### installing docker on linux 

```
[root@ip-172-31-5-47 ~]# yum install docker -y 
Failed to set locale, defaulting to C
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
amzn2-core                                                                                                                            | 3.7 kB  00:00:00     
Resolving Dependencies
--> Running transaction check
---> Package docker.x86_64 0:20.10.23-1.amzn2.0.1 will be installed
--> Processing Dependency: runc >= 1.0.0 for package: docker-20.10.23-1.amzn2.0.1.x86_64
--> Processing Dependency: libcgroup >= 0.40.rc1-5.15 for package: docker-20.10.23-1.amzn2.0.1.x86_64
--> Processing Dependency: containerd >= 1.3.2 for package: docker-20.10.23-1.amzn2.0.1.x86_64
--> Processing Dependency: pigz for package: docker-20.10.23-1.amzn2.0.1.x86_64
--> Running transaction check

```

### starting docker 

```
[root@ip-172-31-5-47 ~]# for i in `cat users.txt`
> do
> usermod -aG docker $i
> done
[root@ip-172-31-5-47 ~]# systemctl enable --now docker 
Created symlink from /etc/systemd/system/multi-user.target.wants/docker.service to /usr/lib/systemd/system/docker.service.
[root@ip-172-31-5-47 ~]# 



```
