# ubuntu-systemd
ubuntu systemd

##### docker build
```
docker build --tag anti1346/ubuntu2204:systemd --no-cache .
```
##### docker push
```
docker push anti1346/ubuntu2204:systemd
```
##### 컨테이너 실행
```
docker run -it --rm anti1346/ubuntu2204:systemd
```
##### Privileged 모드로 컨테이너 실행
```
docker run --privileged --name ubuntu-systemd -d anti1346/ubuntu2204:systemd
```
##### 컨테이너 접속(진입)
```
docker exec -it ubuntu-systemd /bin/bash
```

## docker-ubuntu-sshd(ssh server)
#### docker build
```
docker build --tag anti1346/ubuntu2204:systemd --build-arg SSH_ROOT_PASSWORD=rootpw ./Dockerfile
```

#### docker-compose build
```
docker-compose build --no-cache
```
```
docker-compose up -d; docker-compose ps; docker-compose logs -f
```
```
docker-compose up --build -d; docker-compose ps; docker-compose logs -f
```

###### docker container ip
```
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ssh-server
```
#### ssh access info
root / root
