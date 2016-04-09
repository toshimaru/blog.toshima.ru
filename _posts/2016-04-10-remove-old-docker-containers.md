---
title: Remove old docker containers 
tags: docker
---

When you run `docker ps -a`, you might have too many containers and want to remove old containers. you can remove those continers as below:

```bash
docker rm `docker ps -aq`
```

If specified continer is running, you will get an error:

```
Failed to remove container (f6259edb8236): Error response from daemon: Conflict, You cannot remove a running container. Stop the container before attempting removal or use -f
```

## See also
[How to remove old Docker containers - Stack Overflow](http://stackoverflow.com/questions/17236796/how-to-remove-old-docker-containers)
