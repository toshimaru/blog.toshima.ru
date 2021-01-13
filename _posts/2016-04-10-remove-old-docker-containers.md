---
layout: post
title: Remove old Docker containers
tags: docker
last_modified_at: 2021-01-13
---

**[Update]**

> Since Docker 1.13.x you can use Docker container prune:
> ```
> docker container prune
> ```

[How to remove old Docker containers - Stack Overflow](https://stackoverflow.com/questions/17236796/how-to-remove-old-docker-containers)

## docker prune commands

```console
$ docker container prune
```

```console
$ docker system prune
```

## Reference

- [docker container prune \| Docker Documentation](https://docs.docker.com/engine/reference/commandline/container_prune/)
- [docker system prune \| Docker Documentation](https://docs.docker.com/engine/reference/commandline/system_prune/)

---

When you run `docker ps -a`, you might have too many containers and want to remove old containers. you can remove those containers as below:

```bash
$ docker rm `docker ps -aq`
```

If specified container is running, you'll get an error:

```
Failed to remove container (f6259edb8236): Error response from daemon: Conflict, You cannot remove a running container. Stop the container before attempting removal or use -f
```
