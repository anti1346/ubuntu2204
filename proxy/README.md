# Proxy Server(squid)

#### docker build
```
docker buildx create --use
```
```
docker buildx build --no-cache --platform linux/amd64,linux/arm64 --tag anti1346/ubuntu2204:proxy . --push
```

#### docker 컨테이너 squid 디렉토리
```
/etc/squid/squid.conf
/etc/squid/allowed_ips.txt
/etc/squid/allowed_domains.txt
```

#### Squid Proxy 컨테이너를 리로드
```
squid -k reconfigure
```
