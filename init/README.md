# ubuntu-init

### docker buildx
```
docker buildx create --use
```
```
docker buildx build --platform linux/amd64,linux/arm64 --tag anti1346/ubuntu2204:init --no-cache --push .
```

### docker container run
```
docker inspect anti1346/ubuntu2204:init --format='{{.Architecture}}'
```

### docker container run
```
docker run -itd --privileged --name ubuntu-init --hostname ubuntu-init anti1346/ubuntu2204:init
```


### entering a running docker container
```
docker exec -it ubuntu-init bash
```

<details>
<summary>Docker Build 명령어</summary>

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