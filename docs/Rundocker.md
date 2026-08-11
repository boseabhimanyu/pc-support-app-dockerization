# Mongodb installed in the system

## Docker build and run backend

```
docker build -t pc-support-backend:dev .

docker ps -a

```
### Remove image 

```
docker rm pc-support-backend
```

```
docker run \
  --name pc-support-backend \
  --add-host=host.docker.internal:host-gateway \
  --env-file .env \
  -p 6543:6543 \
  pc-support-backend:dev
```

### Expected error

* 2026/08/11 05:42:29 DB Error: mongo ping failed: server selection error: context deadline exceeded, current topology: { Type: Unknown, Servers: [{ Addr: host.docker.internal:27017, Type: Unknown, Last error: dial tcp 172.17.0.1:27017: connect: connection refused }, ] } *

  ### Check existing Mongo config
  ```
  sudo mongosh --eval 'db.adminCommand({getCmdLineOpts: 1})'
  ```
  ```
  ss -lntp | grep 27017
  
  ```

### Edit mongocofig file

  ```
  sudo nano /etc/mongod.conf

  ```

  ```
  net:
  port: 27017
  bindIp: 127.0.0.1,172.17.0.1

  ```

  ### Expected result -

  {
  argv: [ '/usr/bin/mongod', '--config', '/etc/mongod.conf' ],
  parsed: {
    config: '/etc/mongod.conf',
    net: { bindIp: '127.0.0.1,172.17.0.1', port: 27017 },
    processManagement: { timeZoneInfo: '/usr/share/zoneinfo' },
    storage: { dbPath: '/var/lib/mongodb' },
    systemLog: {
      destination: 'file',
      logAppend: true,
      path: '/var/log/mongodb/mongod.log'
    }
  },
  ok: 1
}

## Check inside Image

```
docker exec -it pc-support-backend sh
```
```
ls -la /app
```
### 
check if env variablers are loaded
```
env | grep -E 'MONGO|PORT|JWT|GIN'
```
```
exit
```
### Check image SHA256 and details

```
docker inspect pc-support-backend --format '{{.Image}}'
```
```
docker images pc-support-backend:dev
```
#### Expected result 

` pc-support-backend:dev   <Unique ID>         67MB           22MB    U   `

------------------------------------------------------------------------------

#### Change docker context

** If required **

```
docker context ls
docker context use desktop-linux
docker context use default

```

#### Docker images list 

```
docker ps -a

```