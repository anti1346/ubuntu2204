# docker ssh(sshd) server

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
##### docker run
```
docker run -d --name ubuntu-sshd anti1346/ubuntu2204:sshd
```
##### docker exec
```
docker exec -it ubuntu-sshd bash
```

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
##### docker container ip
```
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ubuntu-sshd
```
##### ssh access info
ubuntu / ubuntu