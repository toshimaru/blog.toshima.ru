---
layout: post
title: Docker build without cache
tags: docker
---

## docker

```console
$ docker build . --no-cache
```

## docker compose

```console
$ docker compose build [your-service-name] --no-cache
```

## References

- [docker buildx build \| Docker Docs](https://docs.docker.com/reference/cli/docker/buildx/build/)
- [docker compose build \| Docker Docs](https://docs.docker.com/reference/cli/docker/compose/build/)
