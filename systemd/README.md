# docker systemd

## docker
#### Docker Buildx 생성 및 활성화
```
docker buildx create --use
```
####  다중 플랫폼 이미지 빌드 및 레지스트리 푸시(PUSH)
```
docker buildx build --platform linux/amd64,linux/arm64 --tag anti1346/ubuntu2204:systemd --no-cache --push .
```
#### 이미지 풀(PULL)
```
docker pull anti1346/ubuntu2204:systemd
```
#### 빌드된 이미지의 아키텍처 확인
```
docker inspect anti1346/ubuntu2204:systemd --format='{{.Architecture}}'
```
#### 컨테이너를 실행
```
docker run -d --privileged --name ubuntu-systemd anti1346/ubuntu2204:systemd
```
#### 컨테이너 실행
```
docker exec -it ubuntu-systemd bash
```
#### 컨테이너에 Bash 셸 실행
```
docker run -d --privileged --name ubuntu-systemd anti1346/ubuntu2204:systemd
```

#### ssh access info
root / root

<details>
<summary>Docker Compose 코드</summary>
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

</details>

<details>
<summary>README 백업</summary>
  
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
</details>
