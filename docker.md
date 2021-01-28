# Docker

Save docker image to tar.gz archive:

```bash
docker save myimage:latest | gzip > myimage_latest.tar.gz
```

Connect to running docker container:

```bash
docker exec -it <container-id> bash
```
