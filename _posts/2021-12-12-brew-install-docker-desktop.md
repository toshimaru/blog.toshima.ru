---
layout: post
title: Install Docker Desktop via brew install
tags: docker macos
last_modified_at: 2025-08-12
---

## Updates

- 2025-08-12: Use `docker-desktop` instead of `docker`

## Install Docker Desktop via brew

```console
$ brew install docker-desktop
```

~~Dont' forget add `--cask` option since there're formula and cask for docker.~~

After the installation, you can see `✔` mark next to `docker-desktop`.

```console
$ brew search docker
==> Formulae
docker                            docker-credential-helper          docker-machine-driver-vmware      dockerfile-language-server        powerman-dockerize
docker-buildx                     docker-credential-helper-ecr      docker-machine-driver-vultr       dockerfilegraph                   ducker
docker-clean                      docker-gen                        docker-machine-nfs                dockerfmt                         decker
docker-completion                 docker-ls                         docker-machine-parallels          dockerize                         dockly
docker-compose                    docker-machine                    docker-squash                     lazydocker                        mockery

==> Casks
docker-desktop ✔                  docker-toolbox                    dockey                            dockx                             dozer
```
