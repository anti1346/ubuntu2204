# ubuntu-init

### docker build
```
docker buildx create --use
```
```
docker buildx build --platform linux/amd64,linux/arm64 --tag anti1346/ubuntu2204:init --no-cache --push .
```

### docker container run
```
docker run -itd --privileged --name ubuntu-init --hostname ubuntu-init anti1346/ubuntu2204:init
```
```
docker run -d --privileged --name ubuntu-systemd anti1346/ubuntu2204:init
```
```
docker exec -it ubuntu-systemd bash
```

### entering a running docker container
```
docker exec -it ubuntu-init bash
```

<details>
<summary>Docker 코드</summary>

### docker build
```
docker build -t anti1346/ubuntu2204:init --no-cache .
```

```
docker pull anti1346/ubuntu2204:init
```

### docker container run
```
docker run -itd --privileged --name ubuntu-init --hostname ubuntu-init anti1346/ubuntu2204:init
```

### entering a running docker container
```
docker exec -it ubuntu-init bash
```
</details>