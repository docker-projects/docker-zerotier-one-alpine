# zerotier-one-docker

Docker container to run ZeroTier One using Docker.


## For ARM and Raspberry

```
 docker run \                                                                                                                                                 
  -d \
  --name zerotier \
  --device /dev/net/tun \
  --net host \
  --cap-add NET_ADMIN \
  --cap-add SYS_ADMIN \
  -v $HOME/docker/zerotier-alpine:/var/lib/zerotier-one \
    ugeek/zerotier:arm-1.6.3
```



## Run
Spawn the container in background:

```bash
docker run \
  -d \
  --restart unless-stopped \
  --name zerotier-one \
  --device /dev/net/tun \
  --net host \
  --cap-add NET_ADMIN \
  --cap-add SYS_ADMIN \
  -v /var/lib/zerotier-one:/var/lib/zerotier-one \
  henrist/zerotier-one
```



## docker-compose

```
services:
  zerotier:
    image: ugeek/zerotier:arm
    container_name: zerotier
    devices:
      - /dev/net/tun
    network_mode: host
    cap_add:
      - NET_ADMIN
      - SYS_ADMIN
    volumes:
      - $HOME/docker/zerotier:/var/lib/zerotier-one

```





Show status of the service:

```bash
docker exec zerotier-one zerotier-cli status
```

Join a specific network:

```bash
docker exec zerotier-one zerotier-cli join NETWORK-ID
```

## Inspiration

See https://github.com/zyclonite/zerotier-docker
