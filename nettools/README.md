# ubuntu-nettools

##### docker build
```
docker build --tag anti1346/ubuntu2204:nettools . --no-cache
```
##### docker build arg
```
docker build --tag anti1346/ubuntu2204:nettools --build-arg SSH_USER=ubuntu --build-arg SSH_PASSWORD=ubuntu . --no-cache
```
##### docker push
```
docker push anti1346/ubuntu2204:nettools
```
##### docker tag(도커 이미지 태그 이름 변경)
```
docker tag anti1346/ubuntu2204:nettools anti1346/ubuntu-nettools:latest
```
##### docker run test
```
docker run -it --rm --name nettools -h nettools anti1346/ubuntu2204:nettools
```
```
docker run -it --rm --net=host --cap-add net_admin --name nettools anti1346/ubuntu2204:nettools
```
