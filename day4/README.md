# k8s-cloud4c-b3

### k8s client and control plane relation 

<img src="conn.png">

### local and remote client possiblity 

<img src="po.png">

### Kubectl download in windows system as kubernetes client tool 

[click_here](https://kubernetes.io/docs/tasks/tools/)

### verify it 

```
                                                                PS C:\Users\humanfirmware> cd .\Downloads\
PS C:\Users\humanfirmware\Downloads> .\kubectl.exe  version --client
WARNING: This version information is deprecated and will be replaced with the output from kubectl version --short.  Use --output=yaml|json to get the full version.
Client Version: version.Info{Major:"1", Minor:"27", GitVersion:"v1.27.3", GitCommit:"25b4e43193bcda6c7328a6d147b1fb73a33f1598", GitTreeState:"clean", BuildDate:"2023-06-14T09:53:42Z", GoVersion:"go1.20.5", Compiler:"gc", Platform:"windows/amd64"}
Kustomize Version: v5.0.1
PS C:\Users\humanfirmware\Downloads> .\kubectl.exe  version --client   -o yaml
clientVersion:
  buildDate: "2023-06-14T09:53:42Z"
  compiler: gc
  gitCommit: 25b4e43193bcda6c7328a6d147b1fb73a33f1598
  gitTreeState: clean
  gitVersion: v1.27.3
  goVersion: go1.20.5
  major: "1"
  minor: "27"
  platform: windows/amd64
kustomizeVersion: v5.0.1

PS C:\Users\humanfirmware\Downloads> .\kubectl.exe  version --client   -o json
{
  "clientVersion": {
    "major": "1",
    "minor": "27",
    "gitVersion": "v1.27.3",
    "gitCommit": "25b4e43193bcda6c7328a6d147b1fb73a33f1598",
    "gitTreeState": "clean",
    "buildDate": "2023-06-14T09:53:42Z",
    "goVersion": "go1.20.5",
    "compiler": "gc",
    "platform": "windows/amd64"
  },
  "kustomizeVersion": "v5.0.1"
}
```
