# ubuntu-init

## docker build
```
docker build -t anti1346/ubuntu2204:init --no-cache .
```

## docker container run
```
docker run -itd --privileged --name ubuntu-init --hostname ubuntu-init anti1346/ubuntu2204:init
```

## entering a running docker container
```
docker exec -it ubuntu-init bash
```
