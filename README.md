# Running Alpine with Docker
Make sure that community packages are enabled by going uncommenting this line in /etc/apk/repositories
```
http://dl-cdn.alpinelinux.org/alpine/v3.22/community
```
Then run
```
apk update
```

Followed by installing docker:
```
apk add docker docker-compose
```

Start and Enable docker service at boot
```
rc-update add docker default
```
