# ubuntu apt-cacher-ng

## ubuntu build
#### Docker build
```
docker buildx create --use
```
```
docker buildx build --no-cache --platform linux/amd64,linux/arm64 --tag anti1346/ubuntu2204:apt-cacher-ng --push .
```
```
docker buildx build --no-cache --platform linux/amd64,linux/arm64 --tag anti1346/ubuntu2204:apt-cacher-ng --push --build-arg SSH_USER=ubuntu --build-arg SSH_PASSWORD=ubuntu .
```
#### Docker pull
```
docker pull anti1346/ubuntu2204:apt-cacher-ng
```
#### Docker container ip
```
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' anti1346/ubuntu2204:apt-cacher-ng
```
#### Docker run
```
docker run -it --rm --name ubuntu anti1346/ubuntu2204:apt-cacher-ng bash
```
#### ssh access info
```
root / root
```
```
ubuntu / ubuntu
```

## Docker Compose build
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
