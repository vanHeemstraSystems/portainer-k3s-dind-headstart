# 100 - k3s with docker-compose (recommended)
```
$ cd containers/k3s-dind/
$ cp sample.docker-compose.yml docker-compose.yml
$ docker-compose up -d
```

Check with the following if the k3s container has started.

```
$ docker ps
```

If started, check the logs of the k3s containers as follows, using the ```[CONTAINER_ID]``` found previously:

***Documentation***: https://docs.docker.com/engine/reference/commandline/container_logs/

```
$ docker container logs --details [CONTAINER_ID]
```

Output from the k3s container logs could be, for example:

```
E0607 13:30:05.916104     
153 summary_sys_containers.go:47] 
Failed to get system container stats for "/docker/a686584549b729120040b599872addc0de3d46f65848eff6d6c49b5d998fb0b1/systemd": 
failed to get cgroup stats for "/docker/a686584549b729120040b599872addc0de3d46f65848eff6d6c49b5d998fb0b1/systemd": 
failed to get container info for "/docker/a686584549b729120040b599872addc0de3d46f65848eff6d6c49b5d998fb0b1/systemd": 
unknown container "/docker/a686584549b729120040b599872addc0de3d46f65848eff6d6c49b5d998fb0b1/systemd"
```

## 100 - Going inside k3s Docker container

Enter the k3s Docker container as follows:

***Note***: You can get the ```CONTAINER_NAME``` (here: k3s) from docker ps command.

```
$ docker exec -it k3s bash
bash-5.0# 
```

### 100 - k3s

Now ***inside*** the k3s container you can check k3s, like so:

```
$ k3s --version
k3s version v1.18.4+k3s1 (97b7a0e9)
```

***Note***: You may have a different version than above.

Check the k3s config (output may differ):

***Documentation***: https://pgillich.medium.com/setup-lightweight-kubernetes-with-k3s-6a1c57d62217

```
$ k3s check-config
Verifying binaries in /var/lib/rancher/k3s/data/3a8d3d90c0ac3531edbdbde77ce4a85062f4af8865b98cedc30ea730715d9d48/bin:
- sha256sum: good
- links: good

System:
- /sbin iptables v1.8.3 (legacy): ok
- swap: should be disabled
- routes: ok

Limits:
- /proc/sys/kernel/keys/root_maxkeys: 1000000

modprobe: can't change directory to '/lib/modules': No such file or directory
error: cannot find kernel config 
  try running this script again, specifying the kernel config:
  set CONFIG=/path/to/kernel/.config or add argument /path/to/kernel/.config
```

### 200 - kubectl

***Documentation***: https://pgillich.medium.com/setup-lightweight-kubernetes-with-k3s-6a1c57d62217

Check for the wellbeing of kubectl (pronounced: Kube Controller) inside the k3s container:

```
$ kubectl --version
Client Version: version.Info{Major:"1", Minor:"18", GitVersion:"v1.18.4+k3s1", GitCommit:"97b7a0e9df2883f08028fb7171c1e62fc1899a0c", GitTreeState:"clean", BuildDate:"2020-06-18T01:30:45Z", GoVersion:"go1.13.11", Compiler:"gc", Platform:"linux/amd64"}
The connection to the server 127.0.0.1:8443 was refused - did you specify the right host or port?
```

***Note***: ```The connection to the server 127.0.0.1:8443 was refused - did you specify the right host or port?```. TO DO: Explain this...

Get Nodes with kubectl (requires: kubeconfig):

```
$ ls
kubeconfig
$ export 
$ kubectl get nodes -o wide

```

more ...
