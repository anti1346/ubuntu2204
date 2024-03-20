# docker ssh(sshd) server

### docker buildx create
```
docker buildx create --use
```
### docker buildx build & push
```
docker buildx build --platform linux/amd64,linux/arm64 --tag anti1346/ubuntu2204:sshd --no-cache --push .
```
### docker inspect
```
docker inspect anti1346/ubuntu2204:sshd --format='{{.Architecture}}'
```
### docker container run
```
docker run -itd --privileged --name ubuntu-sshd --hostname ubuntu-sshd anti1346/ubuntu2204:sshd
```
### entering a running docker container
```
docker exec -it ubuntu-sshd bash
```

<details>
<summary>docker build</summary>

## docker
##### docker build
```
docker build --tag anti1346/ubuntu2204:sshd --no-cache .
```
```
docker build --tag anti1346/ubuntu2204:sshd --build-arg SSH_USER=ubuntu --build-arg SSH_PASSWORD=ubuntu --no-cache .
```
##### docker push
```
docker push anti1346/ubuntu2204:sshd
```
##### docker run(SSH Server)
```
docker run -d -p 2222:22 --name ubuntu-sshd anti1346/ubuntu2204:sshd
```
</details>


<details>
<summary>docker compose build</summary>

## docker-compose
##### docker-compose build
```
docker-compose build --no-cache
```
```
docker-compose up --build -d; docker-compose ps; docker-compose logs -f
```
```
docker-compose up -d; docker-compose ps; docker-compose logs -f
```
```
docker-compose exec ssh-server bash
```
</details>

##### ssh connect
```
ssh ubuntu@localhost -p 2222
```
##### docker run & docker exec
```
docker run -it --rm --name ubuntu-sshd anti1346/ubuntu2204:sshd bash
```
##### docker container ip
```
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ubuntu-sshd
```
##### ssh access info
ubuntu / ubuntu