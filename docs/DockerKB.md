# Docker Commands

` docker build -t pc-support-backend:dev .
ERROR: permission denied while trying to connect to the docker API at unix:///var/run/docker.sock`

check

```
getent group docker
```

####Run


```
sudo usermod -aG docker $USER
```
Logout and login again


### Check running containers

```
docker ps

```
check all containers

```
docker ps -a

```

### Check all images 

```
docker images

```

### Delete Docker Images

```
docker image prune <image identifier>
```