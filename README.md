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


# Mounting SMB share in Alpine
First install CIFS Utils
```
apk add cifs-utils
```
Add entry(ies) to /etc/fstab
```
//192.168.1.188/photos /mnt/nasaret/photos cifs username=superduperuser,password=supersecretpassword,uid=1000,gid=1000,vers=3.0,rw,sec=ntlmssp 0 0
```

Run netmount command to make sure it is mounted on boot
```
rc-update add netmount default
```
