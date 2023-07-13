# ubuntu2204

## ubuntu
#### docker build
```
docker buildx create --use
```
```
docker buildx build --no-cache --platform linux/amd64,linux/arm64 --tag anti1346/ubuntu2204:latest --push . 
```

```
docker buildx build --no-cache --platform linux/amd64,linux/arm64 --tag anti1346/ubuntu2204:latest  --push --build-arg SSH_USER=ubuntu --build-arg SSH_PASSWORD=ubuntu .
```
#### docker run
```
docker run -it --rm --name ubuntu anti1346/ubuntu2204:latest bash
```
#### docker container ip
```
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ubuntu
```
#### ssh access info
ubuntu / ubuntu

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
docker-compose exec ubuntu bash
```
