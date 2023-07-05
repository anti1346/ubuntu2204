# ubuntu-nettools

##### Docker Buildx 활성화
```
docker buildx create --use
```

##### Docker Buildx를 사용하여 이미지를 빌드하고 푸시
```
docker buildx build --no-cache --platform linux/amd64,linux/arm64 --tag anti1346/ubuntu2204:nettools --push .
```

<!-- ##### docker build arg
```
docker build --tag anti1346/ubuntu2204:nettools --build-arg SSH_USER=ubuntu --build-arg SSH_PASSWORD=ubuntu . --no-cache
```

##### docker push
```
docker push anti1346/ubuntu2204:nettools
``` -->

##### docker tag(도커 이미지 태그 이름 변경)
```
docker tag anti1346/ubuntu2204:nettools anti1346/ubuntu-nettools:latest
```

##### docker run test
```
docker run -it --rm --name nettools anti1346/ubuntu2204:nettools bash
```

```
docker run -it --rm --net=host --cap-add net_admin --name nettools anti1346/ubuntu2204:nettools
```
