# Running Docker in Alpine VM
## Installing Docker & Docker compose
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

## Running docker compose on boot
Create a script in local.d
```
nano /etc/local.d/docker_compose.start
```

With this content
```
#!/bin/sh
# Wait a bit to make sure Docker is ready
sleep 10

# Change to the directory where your docker-compose.yml file is
cd /path/to/your/compose

# Start the containers
docker-compose up -d
```

Save and make sure the script is executable
```
chmod +x /etc/local.d/docker_compose.start
```

Enable local boot service
```
rc-update add local
```

# Mounting SMB share in Alpine VM
First install CIFS Utils
```
apk add cifs-utils
```
Add entry(ies) to /etc/fstab, make sure to point to /mnt on both host and guest
```
//192.168.x.x/share /mnt/nasaret/photos cifs username=superduperuser,password=supersecretpassword,uid=1000,gid=1000,vers=3.0,rw,sec=ntlmssp 0 0
```

Run netmount command to make sure it is mounted on boot
```
rc-update add netmount default
```
Restart and double check that the drive is mounted
