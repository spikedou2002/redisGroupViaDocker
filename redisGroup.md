# Build a Redis Group via Docker
## Overview
    Firt build a network:myNet
`docker network create mynet`
    For master , set REDIS_REPLICATION_MODE=master
    REDIS_PASSWORD = 123456
## Redis Image
    We select a image from bitnam so that we can set the redis_config files through environment variables.
    We first pull the image fron Docker_Hub and create a master node:
```bash
docker run -d -p 6379:6379 \
> -v /app/rd1:/bitnami/redis/data \
>-e REDIS_REPLICATION_MODE=master \
> -e REDIS_PASSWORD=123456 \
>-- network mynet --name redis01 \
>bitnami/redis
```
You will find the logs through
`docker log <container_id>`
` Can't open or create append-only dir appendonlydir: Permission denied`

We can fix it by changing the mod of /app
`chmod -R 777 rd1`

Then we create the slave node:
```bash
docker run -d -p 6380:6379 \
  -v /app/rd2:/bitnami/redis/data \
  -e REDIS_REPLICATION_MODE=slave \
  -e REDIS_HOST=redis01 \
  -e REDIS_MASTER_PORT_NUMBER=6379 \
  -e REDIS_MASTER_PASSWORD=123456 \
  -e REDIS_PASSWORD=123456 \
  --network mynet \
  --name redis02 \
  bitnami/redis
```
