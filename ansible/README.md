# ubuntu-ansible

### docker buildx create
```
docker buildx create --use
```

### docker buildx build & push
```
docker buildx build --platform linux/amd64,linux/arm64 --tag anti1346/ubuntu2204:ansible --no-cache --push .
```

### docker inspect
```
docker inspect anti1346/ubuntu2204:ansible --format='{{.Architecture}}'
```

### docker container run
```
docker run -d -p 2222:22 --name ubuntu-ansible anti1346/ubuntu2204:ansible
```

### entering a running docker container
```
docker exec -it ubuntu-ansible bash
```

<details>
<summary>Docker Build 명령어</summary>

### docker build
```
docker build -t anti1346/ubuntu2204:ansible --no-cache .
```

```
docker pull anti1346/ubuntu2204:ansible
```

### docker container run
```
docker run -itd --privileged --name ubuntu-ansible --hostname ubuntu-ansible anti1346/ubuntu2204:ansible
```

### entering a running docker container
```
docker exec -it ubuntu-ansible bash
```
</details>