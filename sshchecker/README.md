# ubuntu2204(sslchecker)

#### docker build
```
docker buildx create --use
```
```
docker buildx build --no-cache --platform linux/amd64,linux/arm64 --tag anti1346/ubuntu2204:sslchecker --push .
```

##### docker run & exe
```
docker run -it --rm --name sslchecker anti1346/ubuntu2204:sslchecker bash
```

###### docker image architecture
```
docker inspect anti1346/ubuntu2204:sslchecker --format='{{.Architecture}}'
```

###### docker container ip
```
docker inspect sslchecker --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}'
```
