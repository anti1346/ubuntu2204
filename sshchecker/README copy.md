# ubuntu2204(sslchecker)

#### docker build
```
docker buildx build --no-cache --platform linux/amd64,linux/arm64 --tag anti1346/ubuntu2204:sslchecker --push .
```

##### docker run & exe
```
docker run -it --rm --name sslchecker anti1346/ubuntu2204:sslchecker bash
```

###### docker container ip
```
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' sslchecker
```
