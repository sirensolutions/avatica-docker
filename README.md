# Avatica docker

## Requirements

Install `BuildKit` 

```bash
export DOCKER_BUILDKIT=1 \
&& docker build --platform=local -o . git://github.com/docker/buildx \
&& mkdir -p ~/.docker/cli-plugins \
&& mv buildx ~/.docker/cli-plugins/docker-buildx
```

## Docker images build

To build the Docker images that will be used on Kubernetes and export the following environment variables:

- `AVATICA_VERSION`: the Avatica version.
- `POSTGRESQL_VERSION`: the Postgresql version.

To build and push avatica-postgresql images, run:

```bash
docker buildx build \
--push \
--platform linux/arm/v7,linux/arm64/v8,linux/amd64  \
--build-arg "AVATICA_VERSION=1.18.0"  \
--build-arg "POSTGRESQL_VERSION=42.0.0"  \
--tag sirensolutions/avatica-postgresql:1.18.0 postgre
```

To build and push avatica images, run:

```bash
docker buildx build \
--push \
--platform linux/arm/v7,linux/arm64/v8,linux/amd64  \
--build-arg "AVATICA_VERSION=1.18.0"  \
--tag sirensolutions/avatica:1.18.0 .
```