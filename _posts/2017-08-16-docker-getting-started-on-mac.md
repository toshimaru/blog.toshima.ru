---
layout: post
title: Get started with docker on Mac
tags: docker mac
---

Let's get started with docker on Mac.

## Install Docker

First of all, install docker.

```
$ brew install docker
```

Then, run `docker info` to make sure [docker](https://docs.docker.com/) is installed.

```console
$ docker info
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
```

Hmm, docker is installed, but it gets error.

## Install Docker Machine

To solve this, we need to create a machine for Docker. let's install [docker-machine](https://docs.docker.com/machine/) with [virtualbox](https://www.virtualbox.org/).

```
$ brew install docker-machine
$ brew cask install virtualbox
```

## Create Docker Machine on Mac

Okay, then, create default machine with virtualbox driver.

```console
$ docker-machine create --driver virtualbox default
Running pre-create checks...
Creating machine...
(default) Copying /Users/toshimaru/.docker/machine/cache/boot2docker.iso to /Users/toshimaru/.docker/machine/machines/default/boot2docker.iso...
(default) Creating VirtualBox VM...
(default) Creating SSH key...
(default) Starting the VM...
(default) Check network to re-create if needed...
(default) Waiting for an IP...
Waiting for machine to be running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH to be available...
Detecting the provisioner...
Provisioning with boot2docker...
Copying certs to the local machine directory...
Copying certs to the remote machine...
Setting Docker configuration on the remote daemon...
Checking connection to Docker...
Docker is up and running!
To see how to connect your Docker Client to the Docker Engine running on this virtual machine, run: docker-machine env default
```

It says:

> run: docker-machine env default

```console
$ docker-machine env default
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://192.168.x.x:xxxx"
export DOCKER_CERT_PATH="/Users/toshimaru/.docker/machine/machines/default"
export DOCKER_MACHINE_NAME="default"
# Run this command to configure your shell:
# eval $(docker-machine env default)
```

The output says:

> Run this command to configure your shell:

```
$ eval $(docker-machine env default)
```

## Docker is ready

Docker is ready to run.

```
$ docker info
Containers: 0
 Running: 0
 Paused: 0
 Stopped: 0
Images: 0
Server Version: 17.06.0-ce
```

Yay! docker command finally works!

## Docker Status

### docker-machine status

```console
$ docker-machine status
Running
$ docker-machine ls
NAME      ACTIVE   DRIVER       STATE     URL                         SWARM   DOCKER        ERRORS
default   -        virtualbox   Running   tcp://192.x.x.x:xxx           v17.06.0-ce
```

### docker status

```console
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
...
```
