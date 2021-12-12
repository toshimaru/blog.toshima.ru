---
layout: post
title: Install Docker Desktop via brew install
tags: docker macos
---

## Install Docker Desktop via brew

```console
$ brew install --cask docker
```

Dont' forget add `--cask` option since there're formula and cask for docker.

After the installation, you can see `✔` mark next to Formulae docker and Casks docker.

```console
$ brew search docker
==> Formulae
docker ✔                          docker-compose-completion         docker-ls                         docker-machine-driver-vmware      docker-machine-parallels          docker2aci
docker-clean                      docker-credential-helper          docker-machine                    docker-machine-driver-vultr       docker-slim                       dockerize
docker-completion                 docker-credential-helper-ecr      docker-machine-completion         docker-machine-driver-xhyve       docker-squash                     lazydocker
docker-compose                    docker-gen                        docker-machine-driver-hyperkit    docker-machine-nfs                docker-swarm                      mockery

==> Casks
docker-edge                                                         docker ✔                                                            docker-toolbox
```

## Reference

[macos - Brew install docker does not include docker engine? - Stack Overflow](https://stackoverflow.com/questions/40523307/brew-install-docker-does-not-include-docker-engine)
