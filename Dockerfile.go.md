# ubuntu-go
ubuntu go(golang)

##### docker build(amd64)
```
docker build --tag anti1346/ubuntu2204:go --no-cache .
```
##### docker build(add: arm64)
```
docker build --build-arg ARCH=arm64 --tag anti1346/ubuntu2204:go-arm --no-cache .
```
##### docker push
```
docker push anti1346/ubuntu2204:go
```
##### docker run
```
docker run -d --name ubuntu-go anti1346/ubuntu2204:go
```
```
docker run -it --rm --name ubuntu-go anti1346/ubuntu2204:go
```
##### docker exec
```
docker exec -it ubuntu-go bash
```
##### 도커 컨테이너 또는 이미지의 상세 정보 확인
```
docker inspect anti1346/ubuntu2204:go
```
##### 도커 이미지 태그명 변경
```
docker image tag anti1346/ubuntu2204:go-arm anti1346/ubuntu2204:go
```





## docker-ubuntu-go(ssh server)
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
```
docker-compose exec ssh-server bash
```
###### docker container ip
```
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ubuntu-go
```
#### ssh access info
ubuntu / ubuntu
