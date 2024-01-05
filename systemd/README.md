# docker systemd

## docker
#### Docker Buildx 생성하고 활성화
```
docker buildx create --use
```
####  Docker Buildx를 사용하여 여러 플랫폼용으로 이미지를 빌드 및 레지스트리(Docker Hub)에 푸시(push)
```
docker buildx build --platform linux/amd64,linux/arm64 --tag anti1346/ubuntu2204:systemd --no-cache --push .
```
#### 이미지의 풀(pull)
```
docker pull anti1346/ubuntu2204:systemd
```
#### 빌드된 이미지의 아키텍처를 확인
```
docker inspect anti1346/ubuntu2204:systemd --format='{{.Architecture}}'
```
#### 컨테이너를 실행
```
docker run -d --privileged --name ubuntu-systemd anti1346/ubuntu2204:systemd
```
#### 컨테이너를 실행
```
docker exec -it ubuntu-systemd bash
```
#### 컨테이너에 대해 새로운 Bash 셸을 실행
```
docker run -d --privileged --name ubuntu-systemd anti1346/ubuntu2204:systemd
```





## docker-compose
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









##### docker build
```
docker build --tag anti1346/ubuntu2204:systemd --no-cache .
```
```
docker build --tag anti1346/ubuntu2204:systemd --build-arg SSH_ROOT_PASSWORD=rootpw -f ./Dockerfile .
```
##### docker push
```
docker push anti1346/ubuntu2204:systemd
```
##### Privileged 모드로 컨테이너 실행
```
docker run -d --privileged --name ubuntu-systemd anti1346/ubuntu2204:systemd
```
##### 컨테이너 접속(진입)
```
docker exec -it ubuntu-systemd bash
```

##### Privileged 모드로 컨테이너 실행 후 컨테이너에 액세스(접속)
```
docker run -it --rm --privileged --name ubuntu-systemd anti1346/ubuntu2204:systemd bash
```
