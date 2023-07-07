# ubuntu2204(sslchecker)

#### docker build
```
docker buildx create --use
```
```
docker buildx build --no-cache --platform linux/amd64,linux/arm64 --tag anti1346/ubuntu2204:sslchecker --push .
```

###### docker image architecture
```
docker inspect anti1346/ubuntu2204:sslchecker --format='{{.Architecture}}'
```

###### docker image architecture
```
docker run -d -p 8080:80 --name sslchecker anti1346/ubuntu2204:sslchecker
```

##### docker run & execute
```
docker exec -it --rm --name sslchecker bash
```

###### docker container ip
```
docker inspect sslchecker --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}'
```
