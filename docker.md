# Docker

Saving docker image:

```bash
# Saving to a tar archive:
docker save -o myimage_latest.tar myimage:latest

# Saving to a tar.gz archive:
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

## Build

Build docker image:
```bash
DOCKER_BUILDKIT=1 docker build -t <image-tag> -f Dockerfile --progress tty .
```

### Building for another platform

The easiest (but the slowest) way:
```
# Install QEMU:
sudo apt-get update
sudo apt-get install qemu qemu-user-static binfmt-support

# Build arm64 image on amd64 platform:
docker build -t your-image-name:arm64 --platform linux/arm64 .
```

## Run

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

## Cleanup

```
docker image prune
docker system prune
```
