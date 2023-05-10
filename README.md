# ubuntu2204

## ubuntu-sshd(ssh server)
#### docker build
```
docker build --tag anti1346/ubuntu2204:sshd --build-arg SSH_USER=ubuntu --build-arg SSH_PASSWORD=ubuntu --no-cache .
```
#### docker-compose build
(or)
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
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ssh-server
```
#### ssh access info
ubuntu / ubuntu
