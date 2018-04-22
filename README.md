# Docker-Env

## Introduction
An easy to use tool to create a temporary docker container for running a task inside a docker environment. (e.g. install some node dependencies, when you do not have installed node on your computer or build a library that requires a ubuntu environment on your fedora pc)
This script mounts your current working directory inside the docker container and starts a shell (e.g. /bin/bash, /bin/ash or /bin/sh) that is running with your user and group id. (The permissions inside the docker container are the same as on your host system).
And if you want to install some dependencies inside the docker container this script also sets the root password to `root`, to easily gain root access.

### tldr
starts a docker container from your defined docker image and:
  - mounts your current working directory inside the container as /data
  - sets your current uid and gid inside the container
  - starts then a shell inside the container with your uid and gid
  - sets the container root password to `root`
  - destroys the docker container on exit

## Usage

```
docker-env <docker-image-name>:<tag>
```

### Examples

- Start a node environment to install some dependencies of your node project in the current folder.
```
user@host:~/project$ docker-env node

To gain root access type "su root". Password: root

user@docker-node:/data$ ls
README.md  package.json
user@docker-node:/data$ node --version
v9.11.1
```

- Run some scripts that require a ubuntu xenial environment
```
docker-env ubuntu:xenial
```

## Installation

```
sudo curl https://raw.githubusercontent.com/schue30/docker-env/master/docker-env.sh -o /usr/local/bin/docker-env
sudo chmod +x /usr/local/bin/docker-env
```

## ToDo's

- create a powershell version for Windows
- support more shells (in the docker container) than bash, ash and sh

