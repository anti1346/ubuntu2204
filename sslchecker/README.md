# ubuntu2204(sslchecker)

#### docker build
```
docker buildx create --use
```
```
docker buildx build --no-cache --platform linux/amd64,linux/arm64 --tag anti1346/ubuntu2204:sslchecker --push .
```

#### docker image architecture
```
docker inspect anti1346/ubuntu2204:sslchecker --format='{{.Architecture}}'
```

#### docker run
##### 원도우
```
docker run -d -p 8080:80 -v ${pwd}/domains.txt:/sslchecker/domains.txt --name sslchecker anti1346/ubuntu2204:sslchecker
```
##### 리눅스
```
docker run -d -p 8080:80 -v $(pwd)/domains.txt:/sslchecker/domains.txt --name sslchecker anti1346/ubuntu2204:sslchecker
```

#### docker run & execute
```
docker exec -it sslchecker bash
```

#### docker container ip
```
docker inspect sslchecker --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}'
```

#### web browser
```
http://locahost:8080
```
