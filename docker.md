# Docker

Save docker image to tar.gz archive:

```bash
docker save myimage:latest | gzip > myimage_latest.tar.gz
```

Connect to running docker container:

```bash
docker exec -it <container-id> bash
```

Run docker container and login with current non-root user:

```bash
docker run -it -u $(id -u):$(id -g) <container-id> /bin/bash
```
