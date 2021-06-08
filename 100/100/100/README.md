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

Enter the k3s Docker container as follows:

***Note***: You can get the ```CONTAINER_NAME``` (here: k3s) from docker ps command.

```
$ docker exec -it k3s bash
bash-5.0# 
```

Now ***inside*** the k3s container you can check k3s config, like so:

```
$ k3s check-config
```
