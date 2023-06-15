# docker ssh(sshd) server

##### docker build
```
docker build --tag anti1346/ubuntu2204:sshd --no-cache .
```
##### docker tag(도커 이미지 태그 이름 변경)
```
docker tag anti1346/ubuntu2204:sshd anti1346/ubuntu2204:sshd:latest
```
##### docker push
```
docker push anti1346/ubuntu2204:sshd
```
##### docker run
```
docker run -it --rm anti1346/ubuntu2204:sshd
```
##### ssh(sshd) start
```
service ssh start
```

## docker vault test
##### docker network
```
docker network create vnetwork
```
##### docker run
```
docker run -it --name vault-server -h vault-server --net vnetwork anti1346/ssh-server:latest bash
```
```
docker run -it --name ssh-server -h ssh-server --net vnetwork anti1346/ssh-server:latest bash
```
```
docker run -it --name ssh-client -h ssh-client --net vnetwork anti1346/ssh-server:latest bash
```
##### ssh(sshd) start
```
service ssh start
```

## docker-ubuntu-sshd(ssh server)
#### docker build
```
docker build --tag anti1346/ubuntu-sshd:22.04 --build-arg SSH_USER=ubuntu --build-arg SSH_PASSWORD=ubuntu ./Dockerfile.ssh
```
#### docker-compose build
(or)
```
docker-compose build --no-cache
```
```
docker-compose up -d; docker-compose ps; docker-compose logs -f
```
```
docker-compose up --build -d; docker-compose ps; docker-compose logs -f
```
```
docker-compose exec ssh-server bash
```
###### docker container ip
```
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ssh-server
```
#### ssh access info
ubuntu / ubuntu