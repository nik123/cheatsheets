# Docker

Save docker image to tar.gz archive:

```bash
docker save myimage:latest | gzip > myimage_latest.tar.gz
```

Load docker from tar.gz archive:
```bash
docker load -i myimage_latest.tar.gz
```

Connect to running docker container:

```bash
docker exec -it <container-id> bash
```

Build docker image:
```bash
DOCKER_BUILDKIT=1 docker build -t <image-tag> -f Dockerfile --progress tty .
```

## run

Run docker container, start interactive shell and rm container after exit:
```
docker run -it --rm <image> /bin/bash
```

Run docker container and login with current non-root user:

```bash
docker run -it -u $(id -u):$(id -g) <image> /bin/bash
```

GPU access:
```bash
# Make all GPUs available inside container:
docker run -it --gpus all <image>

# Select GPUs 0 and 2 (numbers according to nvidia-smi output):
docker run -it --gpus device=0,2 <image>
```
