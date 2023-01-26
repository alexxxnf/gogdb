# GOG Database Docker
## Building image
To build the image, run in the root directory:
```bash
DOCKER_BUILDKIT=1 docker build -t gogdb:x.y.z -f docker/gogdb/Dockerfile .
```

The image exposes HTTP port 3031.

## Running
There is an example [docker-compose.yaml](./docker-compose.yaml)
that shows how to configure services to work together.
